## テーブル定義書

### users

| No | PK | FK | カラム名      | 項目名         | 備考                         | データ型              | NOT NULL | 列制約 |
|----|----|----|---------------|----------------|------------------------------|----------------------|----------|--------|
| 1  | ○  |    | id            | ユーザーID     | 自動採番                     | INT                  | ○        |  |
| 2  |    |    | name          | 氏名           |                              | VARCHAR(50)          | ○        |        |
| 3  |    |    | email         | メールアドレス | ユニーク                     | VARCHAR(255)         | ○        | UNIQUE |
| 4  |    |    | password      | パスワード     | DB保存時は暗号化             | VARCHAR(255)         | ○        |        |
| 5  |    |    | role          | ユーザー種別   | seeker / recruiter           | ENUM('seeker','recruiter') | ○   |        |
| 6  |    |    | created_at    | 作成日時       | 自動設定                     | TIMESTAMP            | ○        | DEFAULT CURRENT_TIMESTAMP |
| 7  |    |    | updated_at    | 更新日時       | 自動更新                     | TIMESTAMP            | ○        | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

---

### job_seekers

| No | PK | FK | カラム名        | 項目名     | 備考                       | データ型 | NOT NULL | 列制約 |
|----|----|----|----------------|------------|----------------------------|----------|----------|--------|
| 1  | ○  | ○  | user_id        | ユーザーID | users.id を参照            | INT      | ○        | ON DELETE CASCADE |
| 2  |    |    | self_pr        | 自己PR     |                            | TEXT     |          |        |
| 3  |    |    | desired_salary | 希望年収   |                            | INT      |          |        |
| 4  |    |    | created_at     | 作成日時   | 自動設定                     | TIMESTAMP | ○        | DEFAULT CURRENT_TIMESTAMP |
| 5  |    |    | updated_at     | 更新日時   | 自動更新                     | TIMESTAMP | ○        | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

---

### recruiters

| No | PK | FK | カラム名      | 項目名       | 備考                       | データ型 | NOT NULL | 列制約 |
|----|----|----|---------------|--------------|----------------------------|----------|----------|--------|
| 1  | ○  | ○  | user_id       | ユーザーID   | users.id を参照            | INT      | ○        | ON DELETE CASCADE |
| 2  |    | ○  | company_id    | 会社ID       | companies.id を参照        | INT      | ○        | ON DELETE CASCADE |
| 3  |    |    | created_at    | 作成日時     | 自動設定                     | TIMESTAMP | ○        | DEFAULT CURRENT_TIMESTAMP |
| 4  |    |    | updated_at    | 更新日時     | 自動更新                     | TIMESTAMP | ○        | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

---

### companies

| No | PK | FK | カラム名      | 項目名     | 備考             | データ型      | NOT NULL | 列制約 |
|----|----|----|---------------|------------|------------------|---------------|----------|--------|
| 1  | ○  |    | id            | 会社ID     | 自動採番         | INT           | ○        |  |
| 2  |    |    | name          | 会社名     |                  | VARCHAR(50)   | ○        |        |
| 3  |    |    | location      | 所在地     |                  | VARCHAR(255)  |          |        |
| 4  |    |    | description   | 事業内容   |                  | TEXT          |          |        |
| 5  |    |    | created_at    | 作成日時   | 自動設定                     | TIMESTAMP     | ○        | DEFAULT CURRENT_TIMESTAMP |
| 6  |    |    | updated_at    | 更新日時   | 自動更新                     | TIMESTAMP     | ○        | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

---

### jobs

| No | PK | FK | カラム名      | 項目名       | 備考               | データ型      | NOT NULL | 列制約 |
|----|----|----|---------------|--------------|------------------|---------------|----------|--------|
| 1  | ○  |    | id            | 求人ID       | 自動採番           | INT           | ○        |  |
| 2  |    | ○  | company_id    | 会社ID       | companies.id       | INT           | ○        | ON DELETE CASCADE |
| 3  |    |    | title         | タイトル     |                    | VARCHAR(200)  | ○        |        |
| 4  |    |    | description   | 仕事内容     |                    | TEXT          | ○        |        |
| 5  |    |    | min_salary    | 最低給与     |                    | INT           | ○        |        |
| 6  |    |    | max_salary    | 最高給与     |                    | INT           |          |        |
| 7  |    |    | created_at    | 作成日時     | 自動設定           | TIMESTAMP     | ○        | DEFAULT CURRENT_TIMESTAMP |
| 8  |    |    | updated_at    | 更新日時     | 自動更新           | TIMESTAMP     | ○        | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

---

### skills

| No | PK | FK | カラム名   | 項目名   | 備考       | データ型      | NOT NULL | 列制約 |
|----|----|----|------------|----------|------------|---------------|----------|--------|
| 1  | ○  |    | id         | スキルID | 自動採番   | INT           | ○        |  |
| 2  |    |    | name       | スキル名 |            | VARCHAR(50)   | ○        |        |
| 3  |    |    | created_at | 作成日時 | 自動設定   | TIMESTAMP     | ○        | DEFAULT CURRENT_TIMESTAMP |
| 4  |    |    | updated_at | 更新日時 | 自動更新   | TIMESTAMP     | ○        | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

---

### job_skills

| No | PK | FK | カラム名   | 項目名       | 備考                    | データ型 | NOT NULL | 列制約 |
|----|----|----|------------|--------------|------------------------|----------|----------|--------|
| 1  | ○  |    | id         | 求人スキルID | 自動採番               | INT      | ○        |  |
| 2  |    | ○  | job_id     | 求人ID       | jobs.id 参照           | INT      | ○        | ON DELETE CASCADE |
| 3  |    | ○  | skill_id   | スキルID     | skills.id 参照         | INT      | ○        | ON DELETE CASCADE |
| 4  |    |    | created_at | 作成日時     | 自動設定               | TIMESTAMP | ○        | DEFAULT CURRENT_TIMESTAMP |
| 5  |    |    | updated_at | 更新日時     | 自動更新               | TIMESTAMP | ○        | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |
|    |    |    |            |              | (job_id, skill_id) の組み合わせは一意 |          |          | UNIQUE(job_id, skill_id) |

---

### applications

| No | PK | FK | カラム名        | 項目名       | 備考                      | データ型 | NOT NULL | 列制約 |
|----|----|----|----------------|--------------|--------------------------|----------|----------|--------|
| 1  | ○  |    | id             | 応募ID       | 自動採番                 | INT      | ○        |  |
| 2  |    | ○  | job_id         | 求人ID       | jobs.id                  | INT      | ○        | ON DELETE CASCADE |
| 3  |    | ○  | job_seeker_id  | 求職者ID     | job_seekers.user_id      | INT      | ○        | ON DELETE CASCADE |
| 4  |    |    | created_at     | 作成日時     | 自動設定                 | TIMESTAMP | ○        | DEFAULT CURRENT_TIMESTAMP |
| 5  |    |    | updated_at     | 更新日時     | 自動更新                 | TIMESTAMP | ○        | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |
|    |    |    |                |              | (job_id, job_seeker_id) の組み合わせは一意 |          |          | UNIQUE(job_id, job_seeker_id) |

---

### favorites

| No | PK | FK | カラム名      | 項目名      | 備考                    | データ型 | NOT NULL | 列制約 |
|----|----|----|---------------|------------|------------------------|----------|----------|--------|
| 1  | ○  |    | id            | お気に入りID | 自動採番               | INT      | ○        |  |
| 2  |    | ○  | job_id        | 求人ID      | jobs.id                | INT      | ○        | ON DELETE CASCADE |
| 3  |    | ○  | job_seeker_id | 求職者ID    | job_seekers.user_id    | INT      | ○        | ON DELETE CASCADE |
| 4  |    |    | created_at    | 作成日時    | 自動設定               | TIMESTAMP | ○        | DEFAULT CURRENT_TIMESTAMP |
| 5  |    |    | updated_at    | 更新日時    | 自動更新               | TIMESTAMP | ○        | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |
|    |    |    |               |             | (job_id, job_seeker_id) の組み合わせは一意 |          |          | UNIQUE(job_id, job_seeker_id) |

---

### scouts

| No | PK | FK | カラム名        | 項目名       | 備考                     | データ型 | NOT NULL | 列制約 |
|----|----|----|----------------|--------------|-------------------------|----------|----------|--------|
| 1  | ○  |    | id             | スカウトID   | 自動採番                | INT      | ○        |  |
| 2  |    | ○  | company_id     | 会社ID       | companies.id            | INT      | ○        | ON DELETE CASCADE |
| 3  |    | ○  | job_id         | 対象求人ID   | jobs.id                 | INT      | ○        | ON DELETE CASCADE |
| 4  |    | ○  | job_seeker_id  | 求職者ID     | job_seekers.user_id     | INT      | ○        | ON DELETE CASCADE |
| 5  |    |    | message        | メッセージ   |                         | TEXT     | ○        |        |
| 6  |    |    | created_at     | 作成日時     | 自動設定                 | TIMESTAMP | ○        | DEFAULT CURRENT_TIMESTAMP |
| 7  |    |    | updated_at     | 更新日時     | 自動更新                 | TIMESTAMP | ○        | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |
|    |    |    |               |             | (job_id, job_seeker_id) の組み合わせは一意 |          |          | UNIQUE(job_id, job_seeker_id) |
