Importance of lifecycle:
- Knowledge of lifecycle: increase overall knowledge of Spring and Aids troubleshooting.
- Professional Development: deeper knowledge of tools, more educated discussions, better architectural decisions.

Three Phases of Lifecycle:
1. Initialization
2. Use
3. Destruction

The INITIALIZATION phase
- Begins with creation of ApplicationContext
- BeanFactory phase
- Bean initialization and instantiation

Loading Bean Definitions:
- Sources:
    - Java Configuration
    - XML configuration
    - Component Scanning and auto configuration
- Priming the Factory:
    - Bean definitions loaded into BeanFactory from all sources
    - Id is used to create the index for the factory
    - BeanFactory only contains references at this point
- Phase Completed:
    - Beans loaded into BranFactory
    - Beans are references and metadata at this point
    - No object instantiation of code yet
    
Bean Factory post-processing (Post-Processors - BFPP):
- Post-Processors:
    - Can modify/transform any bean prior to instantiation
    - Example: property sources placeholders configuration - "${some.config}"
- BeanFactoryPostProcessor Interface:
    - Write custom components to impact BeanFactory - not common
- BFPP and Java Config
    - Bean Definitions must be static
    - Remove risks of side effects of dynamic instances
- Phase Completed:
    - BeanFactory is loaded with references
    - BeanFactory and all beans in it are configured
    - All system-level work is completed in Spring at this point
    
Bean Instantiation (Step Done for Each Bean):
- Construction:
    - Bean instantiated in factory using contructors
    - Correct order to ensure dependencies are done first
- Phase Complete
    - Bean pointer is still referenced in BeanFactory
    - Objects have been constructed
    - Not Available for use yet
    
Setters:
- Post-Initialization Dependency Injection:
    - After all beans have been instantiated
    - SETTERS are called
    - Autowiring occurs (non-constructor based)
    - JavaConfig behaves differently
- Phase Complete:
    - Beans are fully initialized
    - All initial dependencies are injected
    - Beans still not ready for use
    
Bean Post-Processing:
- Final point of configuration manipulation
- Each bean may have additional behaviors added
- Two types of extensible and generic processing: before and after initializer
- Initializer - special case:
    - Second BeanPostProcessor
    - @PostConstruct methods called
- BeanPostProcessor Interface:
    - Allows to inject common behavior
    - Still operates on specific beans
- Phase Complete:
    - Beans instantiated and initialized
    - Dependencies injected
    - BEANS FINALLY READY FOR USE
    
The USE phase:
- Most of the time is spent in this face
- ApplicationContext serves proxies to the original class
- ApplicationContext maintains handle to each bean

The DESTRUCTION phase
- Begins when close is called on ApplicationContext
- Any @PreDestroy method is called
- BEANS ARE NOT DESTROYED - THIS IS JAVA GARBAGE COLLECTION FUNCTION
