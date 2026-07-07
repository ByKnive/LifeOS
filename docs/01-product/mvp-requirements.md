# LifeOS MVP Requirements

## 1. Purpose

The LifeOS MVP exists to validate one core idea:

> Can a lightweight gamified progress system help create motivation while generating useful personal insights?

The MVP should prove that:

* Progress can be captured with minimal effort.
* Gamification can increase engagement.
* Personal data can reveal meaningful patterns.

The MVP is not intended to be a complete life management platform.

---

# 2. MVP Scope

The MVP focuses on four life categories:

## Career

Examples:

* Data Analysis learning
* Professional development
* Portfolio projects

## Wealth

Examples:

* Trading research
* Investment projects
* Income experiments

## Lifestyle

Examples:

* Cooking skills
* Hosting experiences
* Creative hobbies

## Character

Examples:

* Reflection
* Philosophy
* Personal growth
* Self-awareness

---

# 3. Core User Flow

The MVP user flow:

```
Create Project

↓

Create Quest

↓

Complete Quest

↓

Earn XP

↓

Update Progress

↓

Generate Data

↓

Review Insights
```

---

# 4. Functional Requirements

## 4.1 Project Management

The user must be able to:

* Create projects.
* Assign projects to a Life Category.
* Set project status.
* Track project progress.

Project statuses:

* Active
* Paused
* Completed
* Archived

Required project information:

* Project name
* Category
* Description
* Status
* Creation date
* Completion date (optional)

---

## 4.2 Quest Management

The user must be able to:

* Create quests.
* Complete quests.
* Assign quests to projects.
* Earn XP from completion.

Required quest information:

* Quest name
* Project
* Difficulty
* Status
* Completion date
* XP earned

Quest statuses:

* Planned
* Active
* Completed

---

## 4.3 XP System

The MVP will use a simple XP system.

Initial XP values:

| Difficulty |  XP |
| ---------- | --: |
| Easy       |  10 |
| Medium     |  25 |
| Hard       |  50 |
| Milestone  | 100 |

The XP system should be adjustable.

---

## 4.4 Achievement System

The MVP should support basic achievements.

Examples:

Career:

* First dataset completed
* First portfolio project completed

Wealth:

* First trading experiment completed
* 50 backtests completed

Lifestyle:

* First hosted dinner
* 10 recipes learned

Character:

* 30 reflection entries

Achievements should be based on measurable events.

---

## 4.5 Rewards System

The MVP includes optional personal rewards.

Rewards should be tied to meaningful milestones.

Examples:

Small:

* Coffee
* Favorite meal
* Small purchase

Medium:

* Book
* Hobby equipment
* Experience

Rewards are not required for every achievement.

---

# 5. Data Collection Requirements

Every completed quest should generate a dataset entry.

Minimum tracked data:

| Field      | Purpose              |
| ---------- | -------------------- |
| Date       | Timeline analysis    |
| Category   | Area investment      |
| Project    | Project performance  |
| Quest      | Activity completed   |
| XP         | Progress measurement |
| Difficulty | Effort analysis      |
| Time spent | Efficiency analysis  |

Optional future fields:

* Mood
* Energy
* Satisfaction
* Focus level

---

# 6. Dashboard Requirements

The MVP dashboard should answer:

## Progress

* Total XP
* XP by category
* Active projects
* Completed quests

## Balance

* Time/XP distribution across categories
* Neglected areas

## Insights

Initial insights:

* Most active category
* Least active category
* Project completion rate
* XP trends over time

---

# 7. Non-Requirements

The MVP will intentionally exclude:

* Mobile application
* AI coaching
* Social features
* Avatars
* Complex RPG mechanics
* Skill trees
* Automated recommendations
* Notifications
* Public profiles

These may be considered after validating the foundation.

---

# 8. MVP Success Criteria

The MVP is successful if:

1. Logging progress takes less than 30 seconds.
2. The system is used consistently for multiple weeks.
3. The dataset grows naturally.
4. Insights reveal useful personal patterns.
5. The user enjoys interacting with the system.

---

# 9. Future Evolution

After MVP validation:

Potential next steps:

* Interactive web dashboard
* Better visualization
* Skill progression
* Automated insights
* Predictive analytics
* AI assistance

The MVP should provide the foundation for all future versions.
