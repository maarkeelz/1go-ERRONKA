---
layout: default
title: "Databases"
---

# DATABASES — Documentation

## Advantages of Using a Database Management System

We have chosen Microsoft Access to store the information for our streaming platform. Using a **DBMS** (Database Management System) offers several advantages:

| Advantage | Project example | If poorly organized |
|---|---|---|
| Reducing duplication | Storing plan details only once. | Conflicting information may appear. |
| Linking information | Linking accounts, profiles, and viewing records. | It becomes difficult to know who watched what. |
| Maintaining integrity | Linking viewing records to existing profiles and content. | Records linked to nonexistent data may be created. |
| Querying data | Finding what a profile has watched. | Information must be searched manually. |
| Validating data | Rejecting incorrect prices and dates. | Incorrect data may be stored. |
| Simplifying maintenance | Changing a genre’s name in one place. | Different names and confusion may arise. |

## E-R Diagram Proposals

### Proposal 1: Rejected

![Rejected E-R diagram]({{ "/img/datu-baseak/er-eredua-baztertua.jpg" | relative_url }})

First, we created an initial entity–relationship (ER) diagram for the streaming platform. It included accounts, profiles, watch history, subscriptions, plans, episodes, titles, and genres. We rejected this proposal and developed a more detailed version.

### Proposal 2: Selected

![Selected E-R diagram]({{ "/img/datu-baseak/datubaseak.png" | relative_url }})

In the selected proposal, we separated content into films and series, added seasons to organize series episodes, and included subscription renewals. We also defined separate viewing relationships for films and episodes, recording the viewing date and playback progress.

Finally, we specified the relationships and cardinalities between the entities. We chose this second proposal as the basis for our database design.

## Main Design Decisions

- We separated accounts and profiles so that one account can have multiple profiles.
- We linked viewing records to profiles to keep the viewing histories of people sharing an account separate.
- We stored shared content data in the Content table instead of repeating the same information for films and series.
- We organized series into seasons and episodes so that views of each episode can be recorded separately.
- We used the Content_Genres linking table because each piece of content can belong to multiple genres.
- We separated film and episode viewing records into two tables to link each record to the corresponding content type.
- We used the profile, the viewed item, and the viewing date and time as the composite key for viewing records. This allows the same profile to watch the same content at different times, with each viewing recorded separately.

## Description

This database models a streaming platform with films and series. It manages accounts, viewer profiles, subscriptions and payments, the content catalog, and the viewing history of each profile. It is designed in Third Normal Form (3NF).

This streaming platform offers series and movies with three different types of plans:

| Plan | Monthly price | Maximum screens | Video quality |
|---|---|---|---|
| Basic | €8.99 | 1 | HD (720p) |
| Standard | €13.99 | 2 | Full HD (1080p) |
| Premium | €19.99 | 4 | 4K Ultra HD + HDR |

### Accounts and Profiles

An account stores the login data: unique email, password hash, country, and creation date. Each account can have several profiles, one for each person who uses it.

A profile has a name, a Kids flag (Is_Kids), and a maximum age rating. A Kids profile can only see content whose age rating is lower than or equal to that limit.

### Plans, Subscriptions, and Renewals

Plans define the tiers with their monthly price, maximum number of screens, and video quality.

A subscription links an account to a plan and records its dates, status, and automatic renewal setting.

Each subscription has many renewals, each with its billing period, amount, and payment status. An account can have only one active subscription, and only successful renewals extend access.

### Content Catalog

Content holds what is common to every title: title, description, release year, and age rating.

It is specialized into Films, with their duration, and Series. This specialization is total and disjoint, so every title is exactly one of them.

Series are divided into Seasons, and each season contains Episodes with a number, name, and duration. Episodes inherit the age rating of their series.

Genres classify content through the junction table Content_Genres, since a title can have several genres and a genre applies to many titles.

### Viewing History

Film_Views and Episode_Views record what each profile watches, with the date and time and the progress in seconds. This keeps a separate history per profile and allows “continue watching.”

## Making the Relational Model of the Selected E-R Diagram

Next, we converted the selected ER diagram into a relational model, defining each table, its primary key, foreign keys, and attributes.

We organized the information into separate tables for accounts, profiles, plans, subscriptions, renewals, content, genres, films, series, seasons, episodes, and viewing records.

We added the Content_Genres table to link content with multiple genres. We also used composite primary keys in Content_Genres, Film_Views, and Episode_Views.

For viewing records, the key includes the profile, the film or episode, and the viewing date and time, allowing repeated viewings to be recorded separately.

| Entities | PK (Primary Key) | FK (Foreign Key) | Attributes |
|---|---|---|---|
| Accounts | Account_ID | — | Email (UQ), Password_Hash, Creation_Date, Country |
| Profiles | Profile_ID | Account_ID | Profile Name, Is_Kids, Max_Age_Rating |
| Plans | Plan_ID | — | Plan Name, Monthly_Price, Max_Screens, Video_Quality |
| Subscriptions | Subscription_ID | Account_ID, Plan_ID | Start_Date, End_Date, Status, Auto_Renew |
| Renewals | Renewal_ID | Subscription_ID | Renewal_Date, Period_Start, Period_End, Amount, Payment_Status |
| Content | Content_ID | — | Title, Description, Release_Year, Age_Rating, Content_Type |
| Genres | Genre_ID | — | Name (UQ) |
| Content_Genres | Content_ID, Genre_ID | Content_ID, Genre_ID | — |
| Films | Content_ID | Content_ID | Duration_Min |
| Series | Content_ID | Content_ID | — |
| Seasons | Season_ID | Series_ID | Season_Number, Name, UNIQUE (Series_ID, Season_Number) |
| Episodes | Episode_ID | Season_ID | Episode_Number, Name, Duration_Min, UNIQUE (Season_ID, Episode_Number) |
| Film_Views | Profile_ID, Film_ID, Watched_At | Profile_ID, Film_ID | Progress_Sec |
| Episode_Views | Profile_ID, Episode_ID, Watched_At | Profile_ID, Episode_ID | Progress_Sec |

## Normalization (3NF)

### First Normal Form — 1NF

We stored one value per field and kept profiles, genres, episodes, and viewing events in separate records.

### Second Normal Form — 2NF

We checked that non-key attributes depend on the whole primary key, including composite keys in viewing records.

### Third Normal Form — 3NF

We kept descriptive information in its corresponding table to avoid duplication and dependencies between non-key attributes. There are no transitive dependencies.

| Table | Dependency checked |
|---|---|
| Accounts | Account attributes depend on Account_ID. |
| Profiles | Profile attributes depend on Profile_ID; the account email is not repeated here. |
| Plans | Plan attributes depend on Plan_ID. |
| Subscriptions | Subscription data depends on Subscription_ID; plan details remain in Plans. |
| Renewals | Each renewal’s data belongs to its Renewal_ID. |
| Content | Shared content data depends on Content_ID. |
| Film | Film duration depends on the film’s Content_ID. |
| Series | Only the identifier is stored in the structure shown. |
| Seasons | Season attributes depend on Season_ID; the series name is not repeated. |
| Episodes | Episode attributes depend on Episode_ID; descriptive series and season data is not repeated. |
| Genres | The genre name depends on Genre_ID. |
| Content_Genres | Only the two relationship identifiers are stored, without repeated descriptive data. |
| Watches_Film | Progress belongs to a specific viewing; film and profile details are not repeated. |
| Watches_Episode | Progress belongs to a specific viewing; episode and profile details are not repeated. |

## Access Implementation

Rules are necessary to maintain data integrity in our database. They prevent duplicate values, invalid prices and dates, and records linked to accounts or plans that do not exist.

Configuring them before entering data helps keep the information consistent from the beginning. The following table lists the rules we configured in Access.

| Rule | How to enforce it |
|---|---|
| No duplicate email addresses | Unique index and required field. |
| Each profile must belong to an existing account | Foreign key and referential integrity. |
| Each subscription must reference an existing account and plan | Foreign keys and referential integrity. |
| Prices and amounts must not be negative | Validation rule. |
| The end date must not be earlier than the start date | Record-level validation rule. |
| Season numbers must not repeat within the same series | Unique composite index on the series ID and season number. |
| Episode numbers must not repeat within the same season | Unique composite index on the season ID and episode number. |
| Durations must be positive | Validation rule. |
| Playback progress must not be negative | Validation rule. |

### Relationships

![Access Relationships]({{ "/img/datu-baseak/accs-rela.jpg" | relative_url }})
