Mule Extensions XML Parent POM
==============================

This is a parent POM for use in Mule extensions based on the Mule XML SDK introduced with Mule 4.1+.

It provides several defaults that make managing and building connectors easier (dependencies for running and testing it).

##Configuring MUnit for each project
If needed, MUnit can be customized by adding a plugin with any of the needed parameters in each module, [see the complete configuration properties here](https://docs.mulesoft.com/munit/v/2.1/munit-maven-plugin-configuration).

Example of adding dynamic ports:
```xml
<build>
    <pluginManagement>
        <plugins>
            <plugin>
                <groupId>com.mulesoft.munit</groupId>
                <artifactId>munit-extensions-maven-plugin</artifactId>
                <configuration>
                    <dynamicPorts>
                        <dynamicPort>a.dynamic.here</dynamicPort>
                    </dynamicPorts>
                </configuration>
            </plugin>
        </plugins>
    </pluginManagement>
</build>
```

Example of adding dynamic ports, environment variables and also enabling the MUnit plugin to run in `debug` (port 8000) mode to troubleshoot issues in the runtime/plugin dependencies:
```xml
<build>
    <pluginManagement>
        <plugins>
            <plugin>
                <groupId>com.mulesoft.munit</groupId>
                <artifactId>munit-extensions-maven-plugin</artifactId>
                <configuration>
                    <dynamicPorts>
                        <dynamicPort>another.dynamic.port</dynamicPort>
                    </dynamicPorts>
                    <environmentVariables>
                        <MY_ENV>envVar</MY_ENV>
                    </environmentVariables>
                    <argLines>
                        <!-- To debug the runtime or any other plugin through MUnit -->
                        <debugger.argline>-agentlib:jdwp=transport=dt_socket,server=y,address=8000,suspend=y</debugger.argline>
                        <argLine>-Djava.library.path=lib/</argLine>
                        <argLine>-Xmx8192m</argLine>
                        <argLine>-XX:-UseGCOverheadLimit</argLine>
                    </argLines>
                </configuration>
            </plugin>
        </plugins>
    </pluginManagement>
</build>
```