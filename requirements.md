# System Requirements

## System Roles

**Patient:** A patient can join a healthcare service queue and monitor their queue status.

**Authorized Professional:** Any authorized healthcare professional can perform the operational actions required by the system. The system should not restrict these actions based solely on job title.

**Administrator:** An administrator configures the healthcare unit, its services, users, and system settings. Administrative intervention should not be required for routine queue operation.

## Functional Requirements

### FR01 — Patient Registration

The system shall allow a patient to be registered for a healthcare service.

### FR02 — Queue Entry

The system shall create a queue entry when a patient joins a service queue.

### FR03 — Anonymous Queue Identifier

The system shall generate a unique queue identifier that can be displayed publicly without exposing the patient's personal information.

### FR04 — Service Queues

The system shall support multiple service queues within the same healthcare unit.

### FR05 — Queue Priorities

The system shall support configurable priority levels for queue entries.

### FR06 — Automatic Queue Ordering

The system shall automatically determine the next eligible queue entry according to the configured queue rules and priorities.

### FR07 — Queue Status

The system shall maintain the current status of each queue entry.

Supported statuses shall include:

- Waiting
- Called
- In Service
- Completed
- Cancelled
- Absent

### FR08 — Patient Calling

An authorized professional shall be able to call the next eligible patient.

### FR09 — Automatic Queue Update

The system shall automatically update the queue when a patient is called, begins service, completes service, is marked absent, or is cancelled.

### FR10 — Service Start and Completion

An authorized professional shall be able to record the beginning and completion of a service.

### FR11 — Professional Availability

The system shall allow authorized professionals to indicate when they become available or unavailable for service.

### FR12 — Public Queue Display

The system shall provide a public interface showing currently called queue identifiers and other non-sensitive information necessary for patients to identify when they should proceed to service.

### FR13 — Patient Queue Tracking

The system shall allow patients to monitor their queue status using a personal device through a simple access mechanism, such as a QR code.

### FR14 — Waiting Time Estimation

The system shall provide an estimated waiting time based on available operational data.

### FR15 — Service Configuration

An administrator shall be able to configure the services and queues available at the healthcare unit.

### FR16 — User Authorization

An administrator shall be able to authorize and revoke access for system users.

### FR17 — Operational Records

The system shall store the operational events required to reconstruct queue activity and generate service metrics.

### FR18 — Local Operation

Essential queue operations shall remain available when internet connectivity is unavailable.

### FR19 — Data Synchronization

When connectivity is restored, locally stored data shall be synchronized with the configured remote service, when applicable.

### FR20 — Automatic Recovery

After a temporary loss of connectivity, the system shall restore synchronization without requiring the queue to be manually recreated.

## Non-Functional Requirements

### NFR01 — Low Infrastructure Cost

The system shall not require proprietary kiosks, displays, or specialized hardware for its essential operation.

### NFR02 — Local-First Architecture

Essential queue operations shall not depend on continuous internet connectivity.

### NFR03 — Data Minimization

The system shall collect only the personal information necessary for its intended operation.

### NFR04 — Privacy

The system shall not publicly expose sensitive patient information.

### NFR05 — Authentication and Authorization

Operational and administrative functions shall require appropriate authentication and authorization.

### NFR06 — Usability

The core workflow shall be simple enough to be operated by healthcare professionals with limited technical experience.

### NFR07 — Availability

A temporary loss of internet connectivity shall not interrupt essential queue operations.

### NFR08 — Data Consistency

The system shall prevent concurrent operations from producing inconsistent queue or service states.

### NFR09 — Synchronization Reliability

Synchronization mechanisms shall prevent data loss or unintended duplication when connectivity is restored.

### NFR10 — Performance

Queue operations and status updates shall respond quickly enough for normal healthcare service workflows.

### NFR11 — Maintainability

The system shall use a modular architecture and include automated tests and documentation to support maintenance and future development.

### NFR12 — Scalability

The architecture should support expansion from a small healthcare unit to larger deployments without requiring a complete redesign.

---

# Requisitos do Sistema (Português)

## Papéis do Sistema

**Paciente:** O paciente pode entrar em uma fila de atendimento e acompanhar sua situação.

**Profissional Autorizado:** Qualquer profissional de saúde autorizado pode realizar as ações operacionais necessárias ao funcionamento do sistema. Essas ações não devem ser restringidas exclusivamente com base no cargo do profissional.

**Administrador:** O administrador configura a unidade de saúde, seus serviços, usuários e configurações do sistema. A intervenção administrativa não deve ser necessária para a operação cotidiana das filas.

## Requisitos Funcionais

### RF01 — Cadastro do paciente

O sistema deve permitir o registro de um paciente para um serviço de saúde.

### RF02 — Entrada na fila

O sistema deve criar uma entrada na fila quando um paciente ingressar em uma fila de atendimento.

### RF03 — Identificador anônimo da fila

O sistema deve gerar um identificador único para a entrada na fila que possa ser exibido publicamente sem expor informações pessoais do paciente.

### RF04 — Filas de atendimento

O sistema deve permitir múltiplas filas de atendimento dentro da mesma unidade de saúde.

### RF05 — Prioridades da fila

O sistema deve permitir níveis de prioridade configuráveis para as entradas da fila.

### RF06 — Ordenação automática da fila

O sistema deve determinar automaticamente a próxima entrada elegível de acordo com as regras e prioridades configuradas.

### RF07 — Estado da fila

O sistema deve manter o estado atual de cada entrada na fila.

Os estados devem incluir:

- Aguardando
- Chamado
- Em atendimento
- Concluído
- Cancelado
- Ausente

### RF08 — Chamada do paciente

Um profissional autorizado deve poder chamar o próximo paciente elegível.

### RF09 — Atualização automática da fila

O sistema deve atualizar automaticamente a fila quando um paciente for chamado, iniciar o atendimento, concluir o atendimento, for marcado como ausente ou tiver seu atendimento cancelado.

### RF10 — Início e conclusão do atendimento

Um profissional autorizado deve poder registrar o início e a conclusão de um atendimento.

### RF11 — Disponibilidade do profissional

O sistema deve permitir que profissionais autorizados indiquem quando estão disponíveis ou indisponíveis para atendimento.

### RF12 — Painel público da fila

O sistema deve disponibilizar uma interface pública mostrando os identificadores das filas atualmente chamadas e outras informações não sensíveis necessárias para que os pacientes saibam quando devem se dirigir ao atendimento.

### RF13 — Acompanhamento da fila pelo paciente

O sistema deve permitir que o paciente acompanhe sua situação na fila por meio de um dispositivo pessoal, utilizando um mecanismo de acesso simples, como um QR Code.

### RF14 — Estimativa do tempo de espera

O sistema deve fornecer uma estimativa do tempo de espera com base nos dados operacionais disponíveis.

### RF15 — Configuração dos serviços

O administrador deve poder configurar os serviços e filas disponíveis na unidade de saúde.

### RF16 — Autorização de usuários

O administrador deve poder conceder e revogar o acesso de usuários ao sistema.

### RF17 — Registro operacional

O sistema deve armazenar os eventos operacionais necessários para reconstruir a atividade das filas e gerar métricas de atendimento.

### RF18 — Operação local

As operações essenciais das filas devem permanecer disponíveis quando não houver conexão com a internet.

### RF19 — Sincronização de dados

Quando a conexão for restabelecida, os dados armazenados localmente devem ser sincronizados com o serviço remoto configurado, quando aplicável.

### RF20 — Recuperação automática

Após uma interrupção temporária da conexão, o sistema deve restabelecer a sincronização sem exigir que a fila seja recriada manualmente.

## Requisitos Não Funcionais

### RNF01 — Baixo custo de infraestrutura

O sistema não deve exigir totens, painéis proprietários ou equipamentos especializados para seu funcionamento essencial.

### RNF02 — Arquitetura local-first

As operações essenciais das filas não devem depender de conexão contínua com a internet.

### RNF03 — Minimização de dados

O sistema deve coletar apenas as informações pessoais necessárias para seu funcionamento.

### RNF04 — Privacidade

O sistema não deve expor publicamente informações sensíveis dos pacientes.

### RNF05 — Autenticação e autorização

As funções operacionais e administrativas devem exigir autenticação e autorização adequadas.

### RNF06 — Usabilidade

O fluxo principal deve ser simples o suficiente para ser operado por profissionais de saúde com pouca familiaridade com tecnologia.

### RNF07 — Disponibilidade

Uma perda temporária de conexão com a internet não deve interromper as operações essenciais das filas.

### RNF08 — Consistência dos dados

O sistema deve impedir que operações simultâneas produzam estados inconsistentes na fila ou nos atendimentos.

### RNF09 — Confiabilidade da sincronização

Os mecanismos de sincronização devem evitar perda ou duplicação indevida de dados após o restabelecimento da conexão.

### RNF10 — Desempenho

As operações das filas e suas atualizações devem responder rapidamente o suficiente para o fluxo normal de atendimento.

### RNF11 — Manutenibilidade

O sistema deve utilizar uma arquitetura modular e possuir testes automatizados e documentação que facilitem sua manutenção e evolução.

### RNF12 — Escalabilidade

A arquitetura deve permitir a expansão de uma pequena unidade de saúde para implantações maiores sem exigir uma reconstrução completa.
