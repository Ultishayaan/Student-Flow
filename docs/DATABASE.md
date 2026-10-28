# StudentFlow — Database Schema

Target: **Supabase (Postgres)**. Every table has `user_id` and **Row-Level Security (RLS)** so each student only sees their own data. This is critical for a multi-tenant student app.

## Tables (MVP)

- `profiles` — one row per user (extends Supabase's `auth.users`)
- `subjects` — the classes a student has
- `assignments` — homework, assignments, projects, exams
- `tasks` — simple daily activities/to-dos

## SQL

```sql
-- PROFILES: one row per user (links to Supabase's built-in auth.users)
create table profiles (
  id uuid primary key references auth.users on delete cascade,
  full_name text,
  avatar_url text,
  grade_level text,            -- e.g., "10th grade"
  created_at timestamptz default now()
);

-- SUBJECTS: the classes a student has
create table subjects (
  id uuid primary key default gen_random_uuid(),
  user_id uuid references profiles(id) on delete cascade not null,
  name text not null,          -- "Math", "Biology"
  color text default '#6366f1', -- for the color-coded UI
  teacher_name text,
  created_at timestamptz default now()
);

-- ASSIGNMENTS: homework, assignments, projects, exams
create table assignments (
  id uuid primary key default gen_random_uuid(),
  user_id uuid references profiles(id) on delete cascade not null,
  subject_id uuid references subjects(id) on delete set null, -- optional
  title text not null,
  description text,
  type text default 'homework' check (type in ('homework','assignment','project','exam')),
  due_date timestamptz,
  status text default 'todo' check (status in ('todo','in_progress','done')),
  priority text default 'medium' check (priority in ('low','medium','high')),
  estimated_minutes int,
  completed_at timestamptz,
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);

-- TASKS: daily activities ("gym at 5", "study for chem test")
create table tasks (
  id uuid primary key default gen_random_uuid(),
  user_id uuid references profiles(id) on delete cascade not null,
  title text not null,
  due_date date,               -- which day
  time time,                   -- optional time of day
  kind text default 'personal' check (kind in ('study','personal','activity')),
  is_done boolean default false,
  completed_at timestamptz,
  created_at timestamptz default now()
);
```

## Design decisions
- **`user_id` on every table** + RLS → data isolation per student. Enable RLS and add a policy per table, e.g.:
  ```sql
  alter table assignments enable row level security;
  create policy "own rows" on assignments
    for all using (auth.uid() = user_id);
  ```
- **`subject_id` is nullable** on assignments — you can add an assignment without tagging a subject (`on delete set null` keeps assignments if a subject is deleted).
- **Separate `assignments` vs `tasks`**: assignments have a real due date + status flow; tasks are simple daily to-dos. Keeps the mental model clean for teens.
- Enums are done as `text ... check(...)` for simplicity and easy migration.

## Real-time
Enable real-time on `assignments` and `tasks` via Supabase so edits sync live across devices (a locked requirement).
