Activiti BPM Engine module for Ninja framework.
===============================================
Activiti (http://activiti.org/) is a light-weight workflow and Business Process Management (BPM) Platform targeted at business people, developers and system admins. Its core is a super-fast and rock-solid BPMN 2 process engine for Java.

This module helps running activiti inside Ninja framework (http://www.ninjaframework.org/). 

Getting started
---------------

Setup
-----

1) Add the ninja-activiti-module dependency to your pom.xml:

    <dependency>
        <groupId>ir.cafebabe.ninja</groupId>
        <artifactId>ninja-activiti-module</artifactId>
        <version>0.0.1</version>
    </dependency>

2) Install the module in your conf.Module:

    @Override
    protected void configure() {
        install(new ActivitiModule());
    }
    
3) All set! Start Ninja application and activiti engine will be started with an in-memory database and default configs.
you can inject activiti ProcessEngine, FormService, TaskService, ... in your code.

    @Singleton
    public class Sample {
    
        @Inject
        ProcessEngine processEngine;
        @Inject
        FormService formService;
        @Inject
        HistoryService historyService;
        @Inject
        IdentityService identityService;
        @Inject
        RepositoryService repositoryService;
        @Inject
        RuntimeService runtimeService;
        @Inject
        ManagementService managementService;
        @Inject
        TaskService taskService;

    }


Activiti Engine Configurations
------------------------------

1) You can create activiti.cfg.xml in 'conf' directory. This file will be used as a default activiti configurations. for more detail on how to use the file refer to "www.activiti.org/userguide/". 

2) You can also choose the "configuration file" in conf/application.conf.
    
    activiti.cfg.path=conf/my.activiti.cfg.xml
    %test.activiti.cfg.path=conf/mytest.activiti.cfg.xml

3) There is also possibility to set activiti configuration in  conf/application.conf file without providing activiti xml configuration file.

    ...
    activiti.jdbcDriver=org.h2.Driver
    activiti.jdbcUrl=jdbc:h2:mem:activiti;DB_CLOSE_DELAY=1000
    activiti.jdbcUsername=sa
    activiti.jdbcPassword=
    activiti.mailServerHost=localhost
    ...

  consult activiti documents for list of all process engine configurations "www.activiti.org/userguide/".

4) Mixed-mode: You can also mix xml and property configuration. by providing both activiti.cfg.xml file and ninja properties(conf/application.conf). configs in conf/application.conf overrides xml configuration.

5) No configuration: If there was no configuration, the default activiti configurations with an in-memory database will be applied.

Order of applying configurations
-------------------------------

 Step1) If Default activiti.cfg.xml is provided it will be read unless you explicitly set the config file path in  "conf/application.conf" --> activiti.cfg.path=conf/my.activiti.cfg.xml

 Step2) If there are activiti configuration in "conf/application.conf" they will be override xml configurations.

