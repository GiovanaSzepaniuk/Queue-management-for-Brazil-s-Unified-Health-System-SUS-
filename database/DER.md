# Database Design — Entity-Relationship Diagram (ERD)

## 1. Overview

This document presents the initial database design for the **Queue Management System for Brazil's Unified Health System (SUS)**.

The system organizes healthcare queues by service within each healthcare unit. It supports temporary patient visits, professional availability, queue operations, and operational records.

The database will use **PostgreSQL** as its relational database management system.

## 2. Entity-Relationship Diagram

```mermaid
erDiagram
    HEALTHCARE_UNIT {
        int id PK
        string name
    }

    SERVICE {
        int id PK
        int unit_id FK
        string name
        boolean is_active
    }

    QUEUE {
        int id PK
        int service_id FK "UK"
        boolean is_active
    }

    VISIT {
        int id PK
        int unit_id FK
        string access_token_hash
        datetime started_at
        datetime ended_at
    }

    QUEUE_ENTRY {
        int id PK
        int visit_id FK
        int queue_id FK
        string patient_name
        string public_code UK
        string priority
        string status
        datetime entered_at
    }

    PROFESSIONAL {
        int id PK
        string full_name
        string registration_type
        string registration_number
        string registration_state
        boolean is_active
    }

    SERVICE_PROFESSIONAL {
        int service_id PK "FK"
        int professional_id PK "FK"
    }

    USER_ACCOUNT {
        int id PK
        int unit_id FK
        int professional_id FK "UK"
        string email
        string password_hash
        string role
        boolean is_active
    }

    SERVICE_ATTENDANCE {
        int id PK
        int queue_entry_id FK "UK"
        int professional_id FK
        datetime started_at
        datetime ended_at
    }

    QUEUE_EVENT {
        int id PK
        int queue_entry_id FK
        int user_account_id FK
        string event_type
        string previous_status
        string new_status
        datetime occurred_at
    }

    PROFESSIONAL_AVAILABILITY {
        int id PK
        int professional_id FK
        int service_id FK
        string availability_status
        datetime started_at
        datetime ended_at
    }

    HEALTHCARE_UNIT ||--o{ SERVICE : offers
    SERVICE ||--|| QUEUE : has
    HEALTHCARE_UNIT ||--o{ VISIT : registers
    VISIT ||--o{ QUEUE_ENTRY : contains
    QUEUE ||--o{ QUEUE_ENTRY : receives

    SERVICE ||--o{ SERVICE_PROFESSIONAL : includes
    PROFESSIONAL ||--o{ SERVICE_PROFESSIONAL : works_in

    HEALTHCARE_UNIT ||--o{ USER_ACCOUNT : has
    PROFESSIONAL o|--o| USER_ACCOUNT : accesses_system

    QUEUE_ENTRY ||--o| SERVICE_ATTENDANCE : generates
    PROFESSIONAL ||--o{ SERVICE_ATTENDANCE : performs

    QUEUE_ENTRY ||--o{ QUEUE_EVENT : records
    USER_ACCOUNT o|--o{ QUEUE_EVENT : performs

    PROFESSIONAL ||--o{ PROFESSIONAL_AVAILABILITY : has
    SERVICE ||--o{ PROFESSIONAL_AVAILABILITY : applies_to
```

## 3. Business Rules and Constraints

- Each healthcare unit can offer multiple services.
- Each service has one queue within its healthcare unit.
- Each queue entry belongs to one temporary visit and one service queue.
- A visit can have multiple queue entries over time, but only one active entry at a time.
- A patient must finish or leave the current queue before entering another queue during the same visit.
- Patient names are stored in queue entries; no permanent patient account is required.
- Public queue displays must use anonymous identifiers rather than patient names.
- Preferential priority must be assigned or validated by an authorized professional.
- Multiple professionals can work in the same service, and a professional can be associated with multiple services.
- Only authorized user accounts can perform restricted operational actions.
- Passwords must be stored as secure hashes, never as plain text.
- Queue events record relevant operational changes, including status transitions.
- A queue entry can generate at most one service attendance record.

## 4. Important Implementation Constraints

The following rules must also be enforced when implementing the database:

- A unique constraint must ensure that each service has only one queue.
- A partial unique index must prevent a visit from having more than one active queue entry.
- The service associated with a queue entry must belong to the same healthcare unit as its visit.
- A professional's availability for a service must respect their association with that service.
- Access tokens must be unpredictable; only their hashes should be stored.
- Operational records must follow an appropriate data-retention policy.

---

# Modelagem do Banco de Dados — Diagrama Entidade-Relacionamento (DER)

## 1. Visão Geral

Este documento apresenta a modelagem inicial do banco de dados do **Sistema de Gerenciamento de Filas para o Sistema Único de Saúde (SUS)**.

O sistema organiza filas por serviço dentro de cada unidade de saúde. Ele contempla visitas temporárias de pacientes, disponibilidade dos profissionais, operações das filas e registros operacionais.

O banco de dados utilizará **PostgreSQL** como sistema gerenciador de banco de dados relacional.

## 2. Diagrama Entidade-Relacionamento

O diagrama apresentado na seção anterior representa o modelo conceitual e lógico inicial do sistema. Os nomes das entidades e atributos foram mantidos em inglês para padronização com a implementação.

## 3. Regras de Negócio

- Cada unidade de saúde pode oferecer diversos serviços.
- Cada serviço possui uma fila dentro de sua unidade de saúde.
- Cada entrada de fila pertence a uma visita temporária e a uma fila de serviço.
- Uma visita pode possuir várias entradas de fila ao longo do tempo, mas apenas uma entrada ativa por vez.
- O paciente deve finalizar ou sair da fila atual antes de entrar em outra durante a mesma visita.
- O nome do paciente é armazenado diretamente na entrada da fila; não é necessário manter um cadastro permanente de pacientes.
- Os painéis públicos devem utilizar identificadores anônimos, sem exibir os nomes dos pacientes.
- A prioridade preferencial deve ser atribuída ou validada por um profissional autorizado.
- Vários profissionais podem trabalhar no mesmo serviço, e um profissional pode estar associado a vários serviços.
- Somente contas de usuários autorizados podem executar operações restritas do sistema.
- As senhas devem ser armazenadas como hashes seguros, nunca em texto puro.
- Os eventos da fila registram alterações operacionais relevantes, incluindo mudanças de status.
- Cada entrada de fila pode gerar, no máximo, um registro de atendimento.

## 4. Restrições Importantes para a Implementação

As seguintes regras também deverão ser garantidas durante a implementação do banco de dados:

- Uma restrição de unicidade deverá garantir que cada serviço possua apenas uma fila.
- Um índice único parcial deverá impedir que uma visita possua mais de uma entrada de fila ativa.
- O serviço associado a uma entrada de fila deverá pertencer à mesma unidade de saúde da visita.
- A disponibilidade de um profissional em determinado serviço deverá respeitar sua associação com esse serviço.
- Os tokens de acesso deverão ser imprevisíveis; somente seus hashes deverão ser armazenados.
- Os registros operacionais deverão seguir uma política adequada de retenção de dados.
