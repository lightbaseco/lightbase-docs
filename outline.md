# 

## Getting started

* Installing Lightbase  
* SCMs supported  
  * Github  
  * Gitlab  
  * Bitbucket  
* Limiting repositories  
  * Archived repos  
  * Configuration  
  * Mencionar que los public también se escanean  
* Initial index \+ post-index  
* Data curation

## High level architecture

* High level indexing process  
  * Introducción: a diferencia de sistemas de análisis estático, Lightbase traza los flujos de negocio end-to end, incluso cuando estos atraviesan múltiples servicios a traves de llamadas de red, colas de mensajes, etc…. Esto permite vincular las llamadas a servicios externos, llamadas a bases de datos a los flujos concretos del negocio …  
  * Per repo  
  * Cross repo  
  * Initial indexing vs incremental (delta)  
    * Daily reindexing  
    * Real time indexing available through your account manager  
  * Storage

    

* Languages  
  * Listamos todos \+ Kotlin  
  * Mencionamos soporte para los “principales” frameworks web y de bases de datos   
* Application detection rules  
  * Explicación de en qué se basa y que pueden existir falsos positivos


* Entrypoints / use case analysis  
  * Hacemos un análisis por framework de los puntos de entrada HTTP, por librería de colas, y cli. Esto es lo que nos da los flujos de código de toda la aplicación  
  * View detection  
    * Detectamos las vistas de las aplicaciones de frontend, las acciones que permiten y los endpoint a los que llaman  
        
* External interactions  
  * Database access  (access \+ schema reconstruction)  
  * Cross-service calls  
  * Message queues  
  * Counterparties  
  * File access

Infra support

* Lo metemos con el label de “in development”

MCP

* Chat (con otro nombre)  
* Blast radius  
* Data lineage

Security

* Procesamiento de los análisis  
  * Contenedores sandboxed que no se reutilizan  
  *   
* Almacenamiento del código  
  * Encryption in transit y at rest  
  * Per-customer key CMEK  
  * Access tokens externalizados

Data curation

* Motivación de por qué lo necesitamos  
* El hecho de que generalmente Lightbase te lo deja hecho durante el rollout y puede servir para editar cosas que no pillemos en adelante  
* Gestión de bases de datos  
  * Subida del DDL  
* Business Entities  
  * Qué son  
  * Nosotros creamos una primera propuesta, aunque esto es muy específico del lenguaje de la empresa, permitimos editarlo aquí  
* Counterparties edition  
  * Una counterparty puede pertenecer a múltiples  
  * Un counterparty group representa una entidad externa con la que la empresa interactúa, pueden ser de tipo técnico (AWS) o de negocio (proveedores, SaaS contratados, clientes, …)  
* Application management  
  * Application groups  
  * Variables de entorno  
  * Enable/disable  
  * Rename  
* (Message queues)



