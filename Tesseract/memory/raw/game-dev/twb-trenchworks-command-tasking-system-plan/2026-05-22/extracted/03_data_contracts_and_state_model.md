# 03 — Data Contracts and State Model

## Purpose

This file proposes the minimum data contracts needed to support Player General mission assignment, Enemy General virtual budget/spawn policy/difficulty, squad mission state, squad leader task state, member task state, reaction trees, target reservations, and command event logging.

These are C#-style planning contracts, not production code.

---

## Existing enums to reuse

| Existing enum | Reuse for |
|---|---|
| `WarTeamFaction` | Command ownership: Player or Enemy. |
| `WarTeamKind` | Mission eligibility and spawn selection. |
| `WarMemberRole` | Member task/action catalog lookup. |
| `WarOrder` | Initial UI seed / coarse intent. |
| `WarPosture` | Member posture result from tasks/reactions. |
| `ContactState` | Contact escalation and mission triggers. |
| `TeamDecisionKind` | Squad-level output/bias from missions. |
| `HoldReason` | Explanation for hold/stall/pinned/resupply/treating states. |
| `ContactActionKind` | Local contact reaction summary. |
| `TeamTacticalPhase` | Squad tactical phase and debug display. |
| `WarSupportRequestKind` | Support requests: Ammo, Engineer, FireSupport, Medical, Regroup. |

Do not duplicate these with parallel command enums unless the current enum cannot express the needed higher-level concept.

---

## New enums recommended

### `WarSquadMissionType`

```csharp
public enum WarSquadMissionType
{
    None = 0,
    ScoutProbe,
    MarkContact,
    ScreenFlank,
    AssaultLine,
    HoldFightingLine,
    OccupyRifleBay,
    DigIn,
    ImproveTrench,
    BuildConnectTrench,
    ClaimBuildMgPoint,
    MortarSupport,
    CommandRelay,
    SupplyResupply,
    CasualtyResponse,
    RegroupWithdraw,
    ReserveHold
}
```

### `WarMissionStatus`

```csharp
public enum WarMissionStatus
{
    Pending,
    Assigned,
    Active,
    Paused,
    Completed,
    Failed,
    Retasking,
    Cancelled
}
```

### `WarMissionPriority`

```csharp
public enum WarMissionPriority
{
    Low,
    Normal,
    High,
    Emergency
}
```

### `WarGeneralIntent`

```csharp
public enum WarGeneralIntent
{
    Balanced,
    ReconFirst,
    HoldGround,
    BuildDepth,
    AggressivePressure,
    SustainAndRecover,
    CounterAttack,
    Attrition
}
```

### `EnemyDifficultyTier`

```csharp
public enum EnemyDifficultyTier
{
    Recruit,
    Regular,
    Veteran,
    Brutal
}
```

### `EnemyInfoAccessLevel`

```csharp
public enum EnemyInfoAccessLevel
{
    VisibleOnly,
    RecentContactMemory,
    PressureApproximation,
    WeightedOmniscienceLite
}
```

### `MemberTaskType`

```csharp
public enum MemberTaskType
{
    None,
    MoveToSquadTarget,
    MoveToSocket,
    HoldCover,
    ObserveArc,
    MarkContact,
    FireAtContact,
    SuppressContact,
    BoundMove,
    RegroupOnLeader,
    WithdrawToSafePoint,
    DigTrench,
    ImproveTrench,
    BuildHardpoint,
    RepairHardpoint,
    ClearObstacle,
    PlaceObstacle,
    CarrySupply,
    ResupplySquad,
    FetchAmmo,
    TreatWounded,
    CarryStretcher,
    OperateMachineGun,
    OperateMortar,
    SpotForSupport,
    RelayCommand,
    GuardWorker,
    GuardMedic,
    IdleReserve
}
```

### `MemberTaskStatus`

```csharp
public enum MemberTaskStatus
{
    Unassigned,
    Assigned,
    Moving,
    Working,
    Waiting,
    Blocked,
    Completed,
    Failed,
    Interrupted
}
```

### `ReactionTrigger`

```csharp
public enum ReactionTrigger
{
    None,
    BeingAttacked,
    EnemySeen,
    EnemyHeard,
    SuppressionTaken,
    Wounded,
    LowAmmo,
    LowFood,
    LowMedical,
    NoSafePath,
    LeaderDown,
    MissionTargetReached,
    HardpointSocketReached,
    TrenchSocketReached,
    BuildTaskAssigned,
    RetreatOrdered,
    RegroupOrdered
}
```

### `ReactionPolicy`

```csharp
public enum ReactionPolicy
{
    Ignore,
    ReportOnly,
    PauseTaskThenReact,
    InterruptTask,
    OverrideUntilSafe,
    RequestLeaderDecision
}
```

### `CommandClaimKind`

```csharp
public enum CommandClaimKind
{
    MissionTarget,
    FrontAssignment,
    TrenchSocket,
    HardpointSocket,
    HardpointBuildJob,
    SupplyRequest,
    MedicalRequest,
    FireSupportRequest,
    RegroupPoint
}
```

### `CommandEventKind`

```csharp
public enum CommandEventKind
{
    PlayerSquadSpawned,
    EnemySpawnQueued,
    EnemySpawned,
    MissionCandidateScored,
    MissionAssigned,
    MissionRetasked,
    MissionCompleted,
    MissionFailed,
    ClaimCreated,
    ClaimReleased,
    ClaimExpired,
    ClaimDenied,
    SquadLeaderStateChanged,
    MemberTaskAssigned,
    MemberTaskCompleted,
    MemberTaskFailed,
    SupportRequestRaised,
    SupportRequestAccepted,
    SupportRequestCancelled,
    EnemyBudgetChanged,
    EnemySpawnBlocked,
    DifficultyProfileApplied,
    DebugNote
}
```

---

## Core records/classes

### `WarSquadMission`

```csharp
public sealed class WarSquadMission
{
    public int MissionId;
    public int TeamId;
    public WarTeamFaction Faction;
    public WarSquadMissionType Type;
    public WarMissionStatus Status;
    public WarMissionPriority Priority;

    public WarGeneralIntent Intent;
    public WarOrder SeedOrder;
    public WarTeamKind TeamKind;

    public int AssignedTick;
    public int LastUpdatedTick;
    public int RetaskLockedUntilTick;

    public string LaneId;
    public string TargetFrontId;
    public string TargetSectorId;
    public string TargetBlueprintPieceId;
    public string TargetHardpointId;
    public string TargetSocketId;

    public int ClaimTokenId;

    public float Score;
    public string AssignmentReason;
    public string RetaskReason;
    public string FailureReason;

    public TeamDecisionKind[] LikelyDecisionOutputs;
}
```

Notes: `MissionId` should be deterministic and stable for a run. Target fields can be strings initially if current IDs are string-like; otherwise use existing ID types. `ClaimTokenId` can be `0` or `-1` when no claim exists. `AssignmentReason` should be short enough for UI.

### `MissionScoreContext`

```csharp
public readonly struct MissionScoreContext
{
    public readonly int SimTick;
    public readonly WarTeamFaction Faction;
    public readonly WarTeamKind TeamKind;
    public readonly WarOrder SeedOrder;
    public readonly WarGeneralIntent Intent;
    public readonly string SelectedLaneId;
    public readonly ContactState LaneContactState;
    public readonly float LanePressure;
    public readonly float FriendlyDensity;
    public readonly float EnemyPressureEstimate;
    public readonly float SupplyPressure;
    public readonly float CasualtyPressure;
    public readonly float StalledSectorPressure;
    public readonly int EmptyHardpointSockets;
    public readonly int StartedHardpoints;
    public readonly int CompletedHardpoints;
    public readonly int OpenSupportRequests;
    public readonly bool HasSafePath;
    public readonly bool HasClaimableTarget;
}
```

### `AssignmentScoreBreakdown`

```csharp
public sealed class AssignmentScoreBreakdown
{
    public WarSquadMissionType MissionType;
    public float BaseScore;
    public float LaneScore;
    public float DoctrineScore;
    public float ContactScore;
    public float HardpointScore;
    public float SupplyScore;
    public float CasualtyScore;
    public float StallScore;
    public float ClaimPenalty;
    public float TotalScore;
    public string Reason;
}
```

The selected mission’s score breakdown should be available for debug. Full candidate lists can be kept only in debug builds or recent event logs.

---

## Enemy General contracts

### `EnemyDifficultyProfile`

```csharp
public sealed class EnemyDifficultyProfile
{
    public EnemyDifficultyTier Tier;
    public float StartingBudget;
    public float BudgetIncomePerMinute;
    public float MaxBudget;
    public int MinResponseDelayTicks;
    public int MaxResponseDelayTicks;
    public int SpawnCooldownTicks;
    public int SoftTeamCap;
    public int HardTeamCap;
    public float AggressionWeight;
    public float DefenseWeight;
    public float SupportWeight;
    public float CounterPickWeight;
    public float ComebackBudgetMultiplier;
    public float SnowballThrottleMultiplier;
    public float SupplyGenerosity;
    public float TechMixAdvanceRate;
    public EnemyInfoAccessLevel InfoAccess;
    public float InformationNoise;
    public bool CanUseRecentUnseenContactMemory;
    public bool CanPrioritizeHiddenSupportRequests;
}
```

### `EnemyVirtualBudget`

```csharp
public sealed class EnemyVirtualBudget
{
    public float CurrentBudget;
    public float PressureDebt;
    public float ComebackReserve;
    public int LastIncomeTick;
    public int LastSpawnTick;
    public int NextAllowedSpawnTick;
    public string LastBudgetReason;
}
```

### `EnemySpawnCandidate`

```csharp
public sealed class EnemySpawnCandidate
{
    public string TemplateId;
    public WarTeamKind TeamKind;
    public WarOrder SeedOrder;
    public string LaneId;
    public WarSquadMissionType MissionType;
    public float Cost;
    public float Score;
    public string Reason;
}
```

---

## Squad Leader contracts

```csharp
public enum SquadLeaderTaskState
{
    None,
    MovingToAssignment,
    OccupyingPosition,
    FightingFromPosition,
    OpenGroundContact,
    BuildingTrench,
    ImprovingTrench,
    ClaimingHardpoint,
    Resupplying,
    MedicalResponse,
    Retreating,
    Regrouping,
    LeaderDownFallback,
    Stalled
}
```

```csharp
public sealed class SquadBlackboard
{
    public int TeamId;
    public int ActiveMissionId;
    public SquadLeaderTaskState LeaderState;
    public ContactState LocalContactState;
    public string LocalContactId;
    public string CurrentCoverSocketId;
    public string CurrentHardpointId;
    public bool IsPinned;
    public bool HasLowAmmo;
    public bool HasCasualty;
    public bool LeaderIsDown;
    public bool HasSafePath;
    public int LastStateChangeTick;
    public int LastSupportRequestTick;
    public int LastMemberTaskAssignTick;
    public string StateReason;
}
```

---

## Member task contracts

```csharp
public sealed class MemberTask
{
    public int TaskId;
    public int TeamId;
    public int MemberId;
    public WarMemberRole Role;
    public MemberTaskType Type;
    public MemberTaskStatus Status;
    public int AssignedTick;
    public int StartedTick;
    public int CompletedTick;
    public int ExpiresTick;
    public string TargetSocketId;
    public string TargetHardpointId;
    public string TargetContactId;
    public string TargetMemberId;
    public ReactionPolicy InterruptionPolicy;
    public string AssignmentReason;
    public string FailureReason;
}
```

```csharp
public sealed class MemberReactionRule
{
    public WarMemberRole Role;
    public ReactionTrigger Trigger;
    public ReactionPolicy Policy;
    public MemberTaskType PreferredTask;
    public TeamDecisionKind? SquadDecisionHint;
    public HoldReason? HoldReasonHint;
    public int Priority;
    public string DebugText;
}
```

---

## Claim/reservation contracts

```csharp
public sealed class CommandClaimToken
{
    public int ClaimTokenId;
    public CommandClaimKind Kind;
    public WarTeamFaction Faction;
    public int TeamId;
    public int MissionId;
    public string TargetId;
    public string TargetLaneId;
    public string TargetSectorId;
    public int CreatedTick;
    public int ExpiresTick;
    public int LastRenewedTick;
    public bool IsShared;
    public int MaxSharedUsers;
    public string Reason;
}
```

| Claim kind | Default sharing | Notes |
|---|---:|---|
| `MissionTarget` | Usually exclusive | Prevents many squads choosing the same small objective. |
| `FrontAssignment` | Shared by density limit | Several squads can hold a lane, but cap density. |
| `TrenchSocket` | Exclusive | One squad/member work group per small socket. |
| `HardpointSocket` | Exclusive unless hardpoint supports crew slots | MG/mortar/aid sockets define slot count. |
| `HardpointBuildJob` | Exclusive | One engineer crew owns build progress unless assisted intentionally. |
| `SupplyRequest` | One primary responder, optional backup | Prevents every supply team chasing same request. |
| `MedicalRequest` | One primary responder, optional stretcher support | Prevents duplicate medics. |
| `FireSupportRequest` | Shared by support capacity | Mortar/observer logic can be capacity-based. |
| `RegroupPoint` | Shared | Multiple members/squads can regroup. |

---

## Command event log

```csharp
public sealed class CommandEventLogEntry
{
    public int EventId;
    public int SimTick;
    public CommandEventKind Kind;
    public WarTeamFaction Faction;
    public int TeamId;
    public int MissionId;
    public int MemberId;
    public int ClaimTokenId;
    public string LaneId;
    public string TargetId;
    public string Summary;
    public string Detail;
    public float Score;
    public string ReasonCode;
}
```

Example event summaries:

```text
MissionAssigned: Team 14 ScoutProbe lane=North score=83 reason=SelectedLane+NoContact+NeedVisibility
EnemySpawned: Enemy Assault lane=Center mission=HoldFightingLine reason=PlayerPressureHigh budget=42
ClaimDenied: Team 7 hardpoint=MG_A3 reason=AlreadyClaimedByTeam12
MemberTaskFailed: Team 3 member=Porter task=CarrySupply reason=NoSafePath
```

Use fixed ring buffers:

```text
global command log: latest 256 events
per-team command log: latest 16 events
per-member command log: latest 8 events
```

---

## Serialization and determinism notes

Save only stable state: active missions, active claims, enemy virtual budget, difficulty tier/profile ID, squad blackboards, active member tasks if active mode is enabled, and compact command log only if debug save is desired. Do not save full score candidate history, temporary arrays, expired claims, debug-only candidate tables, or wall-clock timestamps.

Use schema versions:

```text
CommandStateVersion = 1
MissionSchemaVersion = 1
EnemyGeneralSchemaVersion = 1
MemberTaskSchemaVersion = 1
```

All timeouts, cooldowns, spawn delays, and claim TTLs should use simulation ticks. When two candidates tie, use stable tie-breakers: higher priority, lower friendly density, older support request, lower stable lane ID, lower team ID, then lower mission enum value. If variety is needed, use a seeded command RNG derived from run seed, sim tick bucket, faction, and lane ID.

---

## Phase 1 data-driven stance

Use static C# catalogs first:

```text
CommandMissionCatalog
EnemyDifficultyCatalog
MemberRoleActionCatalog
ReactionRuleCatalog
HardpointFamilyCompatibilityCatalog
```

Move catalogs to ScriptableObjects only after behavior is stable, Bob wants designer-editable tuning, tests cover defaults, and save-state compatibility is understood.

---

## Minimum data contracts for Gate 1

Gate 1 should add only:

```text
WarSquadMissionType
WarMissionStatus
WarMissionPriority
WarGeneralIntent
EnemyDifficultyTier
EnemyDifficultyProfile
WarSquadMission
AssignmentScoreBreakdown
CommandEventKind
CommandEventLogEntry
CommandEventLog
```

Optional in Gate 1: `CommandClaimToken`. Member task contracts should wait until the squad mission layer is visible and useful.

## Pushback

Do not add every enum and record in this file in one coding pass. The complete model is listed so the architecture stays coherent, but the first implementation gate should only add what it can test immediately.
