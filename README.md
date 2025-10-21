# BoardWatch

Publicly record all condo decisions, meeting minutes, and votes — timestamped, signed, and immutable.


## Core Feautres of the APP

Features:

**Meeting Timeline**: Displays all past and upcoming meetings with agenda, attachments, and zoom link.

**Minutes Archive**: Board or secretary uploads PDF or text minutes; system auto-hashes and stores version history.

**Voting Record**:  Each board motion recorded with member votes (Y/N/Abstain).

**Resident Commentary**: Owners can post public questions under each decision (non-editable thread).

**Change Ledger**: Every upload or edit adds a new version with diff timestamp.

**Search / Filter**: Search by topic, vendor, date, or board member.

**Notifications**: Email/app push when new minutes or decisions are posted.

## Schemas


TABLE meetings (

id SERIAL PRIMARY KEY,

title TEXT,

date TIMESTAMP,

agenda TEXT,

minutes_url TEXT,

hash TEXT,

created_by INT REFERENCES users(id)

);

TABLE motions (

id SERIAL PRIMARY KEY,

meeting_id INT REFERENCES meetings(id),

description TEXT,

vote_result JSONB,   --
{"yes":5,"no":2,"abstain":0}

passed BOOLEAN,

hash TEXT

);

TABLE audit_log (

id SERIAL PRIMARY KEY,

table_name TEXT,

record_id INT,

action TEXT,         --
INSERT/UPDATE

timestamp TIMESTAMP DEFAULT now(),

hash TEXT,

prev_hash TEXT

);
