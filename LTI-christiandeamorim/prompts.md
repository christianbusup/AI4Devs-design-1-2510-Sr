

## 1. Research and analysis
**Prompt:** NotebookLM
Como analista de negocios Busca en internet sobre los sistemas ATS actuales y analiza en base a la definición de esta compañia a la competencia "LTI es una startup que quiere desarrollar el **ATS (Applicant-Tracking System)** del futuro. 

Todavía no hay nada creado, así que toca ponerse el gorro de **product manager** y definir esas funcionalidades clave que harán brillar a LTI por encima de los competidores:

- Aumentar la eficiencia para los departamentos de HR  
- Mejorar la colaboración en tiempo real entre reclutadores y managers  
- Automatizaciones  
- Asistencia de IA en diversas tareas  

Es el momento de hacer **brainstorming**, investigar cuáles pueden ser las claves del éxito, y dejarlo plasmado para el resto del equipo."

## 2. Detect main features
**Prompt:** NotebookLM
Como analista ed negocios encuentra las principales funcionalidades para el sistema ATS de LTI. Teniendo en cuenta el analisis de mercado realizado en el punto anterior.

## 3. Main functionalities
**Prompt:** Gemini 2 pro inside antigravity
You are an expert software analyst. I am building an ATS system, you can find the definition in this file @[description.md] List and briefly describe the most important use cases to implement to achieve basic functionality bsed on te functionalities in this document @[main-functionalities.md] select the main 3 use cases put this text in .md format

## 4. Use case diagram
**Prompt:** Gemini 2 pro inside antigravity
Represent these use cases in the most appropriate diagram type using the plantUML format. Differentiate between visitor users and logged-in users. Following UML syntax and best practices, define and describe everything necessary.


## 5. Use case diagram svg
**Prompt:** Gemini 2 pro inside antigravity
create 1 svg file per use case with de diagram


## 6. Identify Data Model Entities
**Prompt:** Gemini 2 pro inside antigravity
> You are an expert software architect. What are the essential data model entities in the definition of this project, you will find the definition check in all the files inside the project

## 7. Create Entity Relationship Diagram
**Prompt:** Gemini 2 pro inside antigravity
> Create the entity relation diagram of this data models using mermaid

## 8. High-Level System Design (GCP)
**Prompt:** Gemini 2 pro inside antigravity
> continue as an expert software architect lets create a High-level system design definition using google cloud as a principal tool for architecture

## 9. Refine Design with Specific Questions
**Prompt:** Gemini 2 pro inside antigravity
> include answer to this questions 1. What are the main user roles or personas interacting with the system, and how do their workflows differ?
> 2. Are there specific external systems or third-party services beyond Workday, ADP, and calendar integrations that should be included for data exchange or event triggering?
> 3. Which AI-driven features or processes should be explicitly highlighted in the diagram to show their interaction with other components?
> 4. Should the diagram focus more on high-level service interactions or include detailed data flow and event triggers between components?


## 10. Create High-Level System Design Diagram
**Prompt:** DiagramsGPT
> create the high-level system design diagram using this text "put the text high_level_design.md here"

## 10. Create prompt for create c4 diagram
**Prompt:** GPT promt engineer
> necesito crear un prompt en ingles para solicitar la creacion de un diagrama C4 basandose en documentos de arquitectura, uses_cases, y diagrama entidad relacion y aplicando en role experto que corresponda para estos casos 

## 11. Create C4 diagram
**Prompt:** ChatGPT
> You are a senior software architect specialized in system design and documentation. Based on the following input documents:

Architecture documents

Use cases

Entity-Relationship diagrams

Your task is to create a complete and consistent C4 model diagram, covering at least the first three levels of the C4 model:

Context diagram

Container diagram

Component diagram

Please ensure the following:

Use standard C4 notation and clearly label elements.

Infer and organize components logically from the provided use cases and ER diagram.

Reflect responsibilities, data flow, and external dependencies.

If something is missing or ambiguous, make reasonable expert assumptions and explicitly state them.

Respond with:

A structured textual description of each C4 level

Suggested diagram representations (in Markdown with PlantUML or Mermaid if possible)

A summary of assumptions made during interpretation

Input documents: 

## 12. Unify infromation
**Prompt:** Gemini 2 pro inside antigravity
Compilar todos los documentos .md dentro del directorio @LTI-christiandeamorim  en un solo documento LTI-CDP.md siguiendo este orde Descripción breve del software LTI, valor añadido y ventajas competitivas. Explicación de las funciones principales. Añadir un diagrama Lean Canvas para entender el modelo de negocio
Descripción de los 3 casos de uso principales, con el diagrama asociado a cada uno
Modelo de datos que cubra entidades, atributos (nombre y tipo) y relaciones
Diseño del sistema a alto nivel, tanto explicado como diagrama adjunto
Diagrama C4 que llegue en profundidad a uno de los componentes del sistema, el que prefieras