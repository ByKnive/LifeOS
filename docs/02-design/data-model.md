# LifeOS Data Model

## Purpose

The LifeOS data model defines how all information is stored and related.

The primary design goal is to create a structure that:

* Minimizes data duplication.
* Supports long-term analytics.
* Is easy to implement in Excel.
* Can later be migrated to a relational database (e.g., PostgreSQL).
* Serves as the single source of truth for future dashboards and applications.

The model follows one important principle:

> **Store events, not calculations.**

Values such as project progress, total XP, streaks, and levels should always be calculated from the underlying data rather than stored directly.

---

# Design Principles

## Event Driven

LifeOS stores **completed actions** rather than continuously updating calculated values.

Example:

Instead of storing:

```
Project Progress = 45%
```

LifeOS stores:

```
Quest Completed
Date: 2026-07-08
XP Earned: 25
Minutes Spent: 35
```

Everything else can be derived.

---

## Single Source of Truth

Every piece of information should exist only once.

Examples:

* A project's name belongs in the **Projects** table.
* The completion history belongs in **QuestLog**.
* Areas should never be typed manually inside the QuestLog.

---

## Analytics First

The data model is designed to answer questions such as:

* Where do I invest most of my time?
* Which projects maintain momentum?
* Which activities generate the most progress?
* Which life areas receive the least attention?
* How does my behavior change over time?

---

# Entity Relationship Overview

```
Areas
   │
   │ 1:N
   ▼
Projects
   │
   │ 1:N
   ▼
Quests
   │
   │ 1:N
   ▼
QuestLog

Achievements
```

Every completed quest creates a QuestLog entry.

The QuestLog is the primary dataset used for analysis.

---

# Table Definitions

## Areas

Defines the high-level life categories.

Examples:

* Career
* Wealth
* Lifestyle
* Character

### Fields

| Field    | Type    | Description                |
| -------- | ------- | -------------------------- |
| AreaID   | Integer | Unique identifier          |
| AreaName | Text    | Category name              |
| Active   | Boolean | Whether the area is active |

---

## Projects

Projects represent meaningful goals with a beginning and an end.

Examples:

* Become a Data Analyst
* Trading Strategy Portfolio
* Master Italian Cooking

### Fields

| Field       | Type    | Description                         |
| ----------- | ------- | ----------------------------------- |
| ProjectID   | Integer | Unique identifier                   |
| AreaID      | Integer | Related Area                        |
| ProjectName | Text    | Name of project                     |
| Description | Text    | Optional description                |
| Status      | Text    | Active, Paused, Completed, Archived |
| StartDate   | Date    | Date started                        |
| EndDate     | Date    | Completion date (optional)          |

---

## Quests

Quests are actionable tasks that contribute toward a project.

A quest should normally be completable within **15–60 minutes**.

Examples:

* Complete SQL lesson
* Analyze dataset
* Cook a new recipe
* Backtest trading strategy

### Fields

| Field       | Type    | Description                                                    |
| ----------- | ------- | -------------------------------------------------------------- |
| QuestID     | Integer | Unique identifier                                              |
| ProjectID   | Integer | Related project                                                |
| QuestName   | Text    | Quest title                                                    |
| QuestType   | Text    | Learning, Practice, Research, Building, Reflection, Experience |
| Difficulty  | Text    | Easy, Medium, Hard, Milestone                                  |
| XPValue     | Integer | Base XP reward                                                 |
| Status      | Text    | Planned, Active, Completed                                     |
| CreatedDate | Date    | Date created                                                   |

---

## QuestLog

The QuestLog is the most important table in LifeOS.

Every completed quest generates **one** QuestLog record.

The QuestLog represents the user's historical activity and forms the basis for all analytics.

### Fields

| Field          | Type    | Description       |
| -------------- | ------- | ----------------- |
| LogID          | Integer | Unique identifier |
| QuestID        | Integer | Related quest     |
| CompletionDate | Date    | Date completed    |
| MinutesSpent   | Integer | Time invested     |
| XPEarned       | Integer | XP awarded        |

---

## Achievements

Achievements represent meaningful milestones reached through gameplay.

Achievements are automatically unlocked based on predefined conditions.

Examples:

* First Dataset Completed
* First Hosted Dinner
* 1000 Career XP
* 50 Trading Backtests

### Fields

| Field           | Type    | Description        |
| --------------- | ------- | ------------------ |
| AchievementID   | Integer | Unique identifier  |
| AchievementName | Text    | Display name       |
| UnlockDate      | Date    | Date unlocked      |
| XPBonus         | Integer | Optional XP reward |

---

# Relationships

```
Area
    │
    └──────< Projects

Project
    │
    └──────< Quests

Quest
    │
    └──────< QuestLog
```

Relationship summary:

* One Area contains many Projects.
* One Project contains many Quests.
* One Quest can have one or more QuestLog entries.
* Achievements are unlocked independently based on analytics rules.

---

# Derived Metrics

The following values should **never** be stored directly.

Instead, they should always be calculated.

Examples:

* Total XP
* Level
* Project Progress
* Completion Rate
* XP by Area
* XP by Project
* Average Session Length
* Weekly XP
* Monthly XP
* Momentum Score
* Achievement Progress

This ensures the data always remains consistent.

---

# Future Fields

The following fields may be introduced after MVP validation.

## Mood

Scale:

1–5

Purpose:

Analyze whether specific activities improve emotional well-being.

---

## Energy

Scale:

1–5

Purpose:

Analyze when the user performs at their best.

---

## Satisfaction

Scale:

1–5

Purpose:

Measure perceived value after completing an activity.

These fields are intentionally excluded from the MVP to reduce logging friction.

---

# Example Workflow

```
Create Project

↓

Create Quest

↓

Complete Quest

↓

QuestLog Entry Created

↓

Dashboard Updates

↓

Insights Generated
```

---

# Analytics Opportunities

The data model should support analyses such as:

## Category Analysis

* XP by Life Area
* Time invested by Area
* Category balance over time

---

## Project Analysis

* Project completion rate
* Average project duration
* Active vs. completed projects
* Archived project analysis

---

## Quest Analysis

* Completion rate
* Average completion time
* XP distribution
* Difficulty distribution
* Quest type distribution

---

## Productivity Analysis

* XP by weekday
* XP by month
* Time invested per week
* Long-term consistency trends

---

## Personal Insights

Examples:

* Which activities create the highest consistency?
* Which projects are abandoned most frequently?
* Which category has been neglected recently?
* How has personal focus shifted over time?

---

# Future Evolution

The current data model is intentionally minimal.

As LifeOS evolves, additional entities may be introduced, including:

* Rewards
* Skill Trees
* Levels
* Inventory
* Statistics
* AI Recommendations

These additions should extend the existing model rather than replace it.

The foundation of LifeOS will always remain:

**Areas → Projects → Quests → QuestLog**

Everything else is derived from these core entities.
