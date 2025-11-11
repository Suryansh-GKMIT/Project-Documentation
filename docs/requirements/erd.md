# ERD — skillcheck (normalized)

This diagram shows the normalized schema for SkillCheck (roles, users, tests, questions, options, assignments, attempts, and user responses).<br>
PK / FK annotations are included for clarity.<br>

```mermaid
---
config:
  layout: elk
---
erDiagram
	direction LR
	roles {
		bigint id PK ""  
		varchar name  ""  
		timestamp created_at  ""  
		timestamp updated_at  ""  
		timestamp deleted_at  ""  
	}
	users {
		bigint id PK ""  
		varchar name  ""  
		varchar email  ""  
		varchar password_hash  ""  
		timestamp created_at  ""  
		timestamp updated_at  ""  
		timestamp deleted_at  ""  
	}
	roles_users {
		bigint id PK ""  
		bigint role_id FK ""  
		bigint user_id FK ""  
		timestamp created_at ""  
		timestamp updated_at ""  
		timestamp deleted_at ""  
	}
	tests {
		bigint id PK ""  
		varchar title  ""  
		varchar description  ""  
		int duration_minutes  ""  
		varchar status  ""  
		bigint created_by FK ""  
		timestamp created_at  ""  
		timestamp updated_at  ""  
		timestamp deleted_at  ""  
	}
	questions {
		bigint id PK ""  
		bigint test_id FK ""  
		varchar question_text  ""  
		bigint correct_option_id FK ""  
		timestamp created_at  ""  
		timestamp updated_at  ""  
		timestamp deleted_at  ""  
	}
	options {
		bigint id PK ""  
		bigint question_id FK ""  
		varchar content  ""    
		timestamp created_at  ""  
		timestamp updated_at  ""  
		timestamp deleted_at  ""  
	}
	test_assignments {
		bigint id PK ""  
		bigint test_id FK ""  
		bigint user_id FK ""  
		timestamp created_at  ""  
		timestamp updated_at  ""  
		timestamp deleted_at  ""  
	}
	test_attempts {
		bigint id PK ""  
		bigint test_id FK ""  
		bigint user_id FK ""  
		timestamp started_at  ""  
		timestamp ended_at  ""  
		int score  ""  
		timestamp created_at  ""  
		timestamp updated_at  ""  
		timestamp deleted_at  ""  
	}
	user_responses {
		bigint id PK ""  
        bigint user_id FK "" 
		bigint attempt_id FK ""  
		bigint question_id FK ""  
		bigint option_id FK ""   
		boolean is_correct  ""    
		timestamp created_at  "" 
        timestamp updated_at  ""  
		timestamp deleted_at  ""    
	}
	roles ||--o{ roles_users : "assigned to"
	users ||--o{ roles_users : "has"
	users||--o{tests:"creates"
	tests||--o{questions:"contains"
	questions||--o{options:"has options"
	tests||--o{test_assignments:"is assigned to"
	users||--o{test_assignments:"receives assignment"
	test_assignments||--o{test_attempts:"produces attempt"
	users||--o{test_attempts:"takes"
	tests||--o{test_attempts:"attempted in"
	test_attempts||--o{user_responses:"records answers"
	questions||--o{user_responses:"answered in"
	options||--o{user_responses:"selected in"
	users||--o{user_responses:"submitted by"
```
