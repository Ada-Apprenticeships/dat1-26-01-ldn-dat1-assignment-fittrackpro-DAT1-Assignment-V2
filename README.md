# FitTrack Pro — Complete Student Reference (Expected Output)

> Each query file runs on a **fresh database**. Within a file, queries execute in order — INSERT/UPDATE/DELETE statements affect later queries.

---

# 1. User Management

## 1.1 Retrieve all members

```
member_id  first_name  last_name  email                    join_date
---------  ----------  ---------  -----------------------  ----------
1          Alice       Smith      alice.smith@email.com    2023-01-10
2          Bob         Jones      bob.jones@email.com      2023-02-15
3          Charlie     Brown      charlie.brown@email.com  2023-03-20
4          Diana       Prince     diana.prince@email.com   2023-04-25
5          Emily       Jones      emily.jones@email.com    2023-05-10
6          Frank       Castle     frank.castle@email.com   2023-06-15
7          Grace       Lee        grace.lee@email.com      2023-07-20
8          Henry       Ford       henry.ford@email.com     2023-08-05
9          Iris        West       iris.west@email.com      2023-09-10
10         Jack        Ryan       jack.ryan@email.com      2023-10-15
11         Kevin       Mitnick    kevin.mitnick@email.com  2023-11-20
```

11 rows returned.

---

## 1.2 Update member 5's contact information

*Affects 1 row.* No result set — this is an UPDATE statement.

Member 5 (Emily Jones) email changes to `emily.jones.new@email.com` and phone to `555-9999`.

---

## 1.3 Count total members

```
total_members
-------------
11
```

---

## 1.4 Member with most class registrations (Registered status only)

```
member_id  first_name  last_name  registration_count
---------  ----------  ---------  ------------------
5          Emily       Jones      2
```

### Variation 1.4v — All statuses

```
member_id  first_name  last_name  registration_count
---------  ----------  ---------  ------------------
5          Emily       Jones      3
```

---

## 1.5 Member with least class registrations (Registered status only)

```
member_id  first_name  last_name  registration_count
---------  ----------  ---------  ------------------
2          Bob         Jones      1
```

---

## 1.6 Members with ≥2 class attendances (Attended status only)

```
Count
-----
1
```

### Variation 1.6v — Registered + Attended

```
Count
-----
4
```

---

# 2. Payment Management

## 2.1 Record a new payment

*Affects 1 row.* No result set — this is an INSERT statement.

New payment for member 11, amount £50.00, paid via Credit Card.

---

## 2.2 Monthly revenue (November 2024 – January 2025)

```
month    total_revenue
-------  -------------
2024-11  100.0
2024-12  100.0
2025-01  100.0
```

---

## 2.3 Day pass purchases

```
payment_id  amount  payment_date         payment_method
----------  ------  -------------------  --------------
7           20.0    2025-01-20 15:30:00  Cash
```

### Variation 2.3v — Member name included

```
payment_id  member_name    amount  payment_date         payment_method
----------  -------------  ------  -------------------  --------------
7           Kevin Mitnick  20.0    2025-01-20 15:30:00  Cash
```

---

# 3. Equipment Management

## 3.1 Equipment needing maintenance within 30 days of 2025-01-01

```
equipment_id  name            next_maintenance_date
------------  --------------  ---------------------
1             Treadmill 2000  2025-01-15
```

---

## 3.2 Count of equipment by type

```
equipment_type  count
--------------  -----
Cardio          2
Strength        2
```

---

## 3.3 Average age of equipment by type (using current date)

> **Note**: Output is date-sensitive (uses current date).

```
equipment_type  avg_age_days
--------------  ------------
Cardio          <varies>
Strength        <varies>
```

### Variation 3.3v — Fixed date (2025-01-01)

```
equipment_type  avg_age_days
--------------  ------------
Cardio          699.0
Strength        649.0
```

---

# 4. Class Scheduling

> 4.3 (INSERT) and 4.4 (DELETE) modify data before 4.5–4.6 run.

## 4.1 List all classes with instructors

```
class_id  class_name   instructor_name
--------  -----------  ---------------
1         Spin Class   Ivy Irwin
2         Yoga Basics  Lara Croft
3         HIIT         Ivy Irwin
```

### Variation 4.1v — With DISTINCT

Same output (no duplicates in data).

---

## 4.2 Classes available on 2025-02-01

```
class_id  name         start_time           end_time             available_spots
--------  -----------  -------------------  -------------------  ---------------
1         Spin Class   2025-02-01 09:00:00  2025-02-01 09:45:00  18
2         Yoga Basics  2025-02-01 10:00:00  2025-02-01 11:00:00  13
```

---

## 4.3 Enroll member 11 in Spin Class (schedule_id 1)

*Affects 1 row.* No result set — this is an INSERT statement.

---

## 4.4 Cancel member 3's registration for schedule 7

*Affects 1 row.* No result set — this is a DELETE statement (removes the row).

---

## 4.5 Most popular class (Registered status)

```
class_id  class_name  registration_count
--------  ----------  ------------------
1         Spin Class  2
```

### Variation 4.5v — All statuses

```
class_id  class_name  registration_count
--------  ----------  ------------------
1         Spin Class  4
```

---

## 4.6 Average classes per member

```
avg_classes_per_member
----------------------
1.67
```

### Variation 4.6v — Divided by all 11 members

```
avg_classes_per_member
----------------------
0.91
```

---

# 5. Membership Management

## 5.1 Active memberships

```
member_id  first_name  last_name  membership_type  join_date
---------  ----------  ---------  ---------------  ----------
2          Bob         Jones      Premium          2023-02-15
3          Charlie     Brown      Standard         2023-03-20
5          Emily       Jones      Premium          2023-05-10
```

---

## 5.2 Average visit duration by membership type

```
membership_type  avg_visit_duration_minutes
---------------  --------------------------
Premium          82.5
Standard         60.0
```

---

## 5.3 Memberships expiring in 2025

```
member_id  first_name  last_name  email                    end_date
---------  ----------  ---------  -----------------------  ----------
1          Alice       Smith      alice.smith@email.com    2025-01-01
2          Bob         Jones      bob.jones@email.com      2025-06-15
3          Charlie     Brown      charlie.brown@email.com  2025-03-20
5          Emily       Jones      emily.jones@email.com    2025-05-10
```

4 rows (includes expired memberships with 2025 end dates).

### Variation 5.3v — Active only

```
member_id  first_name  last_name  email                    end_date
---------  ----------  ---------  -----------------------  ----------
2          Bob         Jones      bob.jones@email.com      2025-06-15
3          Charlie     Brown      charlie.brown@email.com  2025-03-20
5          Emily       Jones      emily.jones@email.com    2025-05-10
```

3 rows (excludes Alice — Inactive membership).

---

# 6. Attendance Tracking

> 6.1 (INSERT) adds a record before 6.2–6.4 run.

## 6.1 Record member 7's gym visit

*Affects 1 row.* No result set — this is an INSERT statement.

Member 7 (Grace Lee) checks in at Downtown Fitness on 2025-02-14 at 16:30.

---

## 6.2 Attendance history for member 5

```
visit_date  check_in_time        check_out_time
----------  -------------------  -------------------
2025-01-10  2025-01-10 08:00:00  2025-01-10 09:30:00
2025-01-12  2025-01-12 18:00:00  2025-01-12 19:15:00
```

---

## 6.3 Busiest day of the week

```
day_of_week  visit_count
-----------  -----------
Friday       2
```

### Variation 6.3v — All days shown

```
day_of_week  visit_count
-----------  -----------
Friday       2
Sunday       1
Wednesday    1
```

---

## 6.4 Average daily attendance per location (only days with visits)

```
location_name      avg_daily_attendance
-----------------  --------------------
Downtown Fitness   1.0
Suburban Wellness
```

4 visits / 4 distinct visit-days = 1.0

### Variation 6.4v (advanced) — Full date range including zero days

Uses all calendar days between the earliest and latest recorded visit per location (including days with zero attendance). **This variation requires additional self-learning around SQLite date functions and window queries not directly covered in course material.**

```
location_name      avg_daily_attendance
-----------------  --------------------
Downtown Fitness   0.11
Suburban Wellness
```

- Downtown Fitness: 4 visits across 36 days (Jan 10 – Feb 14) → 4/36 = 0.11
- Suburban Wellness: no attendance records → NULL

> **Note:** Both methods are accepted. The simpler method demonstrates core concepts; the advanced variant extends your learning beyond taught material.

---

# 7. Staff Management

## 7.1 List all staff members by position

```
staff_id  first_name  last_name  role
--------  ----------  ---------  ------------
1         James       Bond       Manager
3         Sarah       Connor     Receptionist
2         Ivy         Irwin      Trainer
4         Lara        Croft      Trainer
```

---

## 7.2 Trainers with ≥1 session in 30 days from 2025-01-20

```
trainer_id  trainer_name  session_count
----------  ------------  -------------
2           Ivy Irwin     3
```

### Variation 7.2v — February 2025 only

```
trainer_id  trainer_name  session_count
----------  ------------  -------------
2           Ivy Irwin     1
```

---

# 8. Personal Training

## 8.1 Personal training sessions for trainer "Ivy Irwin"

```
session_id  member_name    session_date  start_time  end_time
----------  -------------  ------------  ----------  --------
1           Alice Smith    2025-01-25    09:00:00    10:00:00
2           Charlie Brown  2025-01-28    14:00:00    15:00:00
3           Emily Jones    2025-02-04    10:00:00    11:00:00
```