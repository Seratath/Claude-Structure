# Pipeline Flow

```mermaid
flowchart TD
    U([User input]) --> PM

    PM{PM: project\nor direct?}
    PM -->|direct answer| ANS([Answer user])
    PM -->|project| S1

    subgraph S1 [Stage 1 · Prompt Improvement]
        PA[Prompt Agent] --> QC1[QC Agent]
        QC1 -->|FAIL| PA
        QC1 -->|PASS| APR1{User approval}
        APR1 -->|reject + feedback| PA
        APR1 -->|stop| STOP([Update workboard · stop])
    end

    APR1 -->|approve| LOG1[Logger Agent]
    LOG1 --> S2

    subgraph S2 [Stage 2 · High-Level Planning]
        PLA1[Planning Agent\nplan mode] --> QC2[QC Agent]
        QC2 -->|FAIL| PLA1
        QC2 -->|PASS| APR2{User approval}
        APR2 -->|reject + feedback| PLA1
    end

    APR2 -->|approve| LOG2[Logger Agent]
    LOG2 --> S3

    subgraph S3 [Stage 3 · Step Breakdown]
        PLA2[Planning Agent\nstep mode\nper plan item] --> QC3[QC Agent]
        QC3 -->|FAIL| PLA2
        QC3 -->|PASS| APR3{User approval}
        APR3 -->|reject + feedback| PLA2
    end

    APR3 -->|approve| LOG3[Logger Agent]
    LOG3 --> S4

    subgraph S4 [Stage 4 · Execution Loop]
        EX[Execution Agent\nproject-specific\nper step] --> QC4[QC Agent]
        QC4 -->|FAIL| EX
        QC4 -->|PASS| APR4{User approval}
        APR4 -->|reject + feedback| EX
    end

    APR4 -->|approve| LOG4[Logger Agent]
    LOG4 --> RM[Repo Manager]
    RM --> CYCLE{More steps?}
    CYCLE -->|yes| S4
    CYCLE -->|no, more phases?| S3
    CYCLE -->|done| GA_CHK[GA milestone review]
    GA_CHK --> DONE([Project phase complete])

    subgraph FAIL_HANDLING [Fail Handling · any stage]
        FAIL[Agent returns FAIL] --> ENV{Environmental?}
        ENV -->|yes, retry once| RETRY[Retry same input]
        RETRY -->|fails again| USER_F{User: retry /\nstop / change?}
        ENV -->|no| USER_F
        USER_F --> RETRO_Q[Log to retrospective queue]
    end

    subgraph RETRO [Retrospective · 2+ same-type rejections]
        RA[Retrospective Agent] --> QC_R[QC Agent]
        QC_R -->|PASS| APR_R{User approves\namendment?}
        APR_R -->|yes| LOG_R[Logger Agent\npatches agent file]
        APR_R -->|no| DISCARD([Discard · log decision])
    end

    subgraph REBASE [Context Rebase · after 1-2 cycles]
        RB1[Write state to protocol/state.md] --> RB2[Write open items to workboard]
        RB2 --> RB3[Compact session summary]
        RB3 --> RB4([Resume from clean state])
    end
```

## Notes

- **QC loops** are tight — FAIL sends back to the same agent with the QC verdict, not to the user
- **User approval** is the only gate that can stop, redirect, or approve
- **Logger Agent** fires post-approval, never blocking
- **Repo Manager** fires post-cycle, never blocking
- **Retrospective** runs in parallel to the main pipeline — it amends agent profiles, not current pipeline state
- **GA** is invoked at phase completion, not within stages
- **Parallel execution** is permitted in Stage 3 and Stage 4 for independent items — each runs as a separate job ID in `work/`
