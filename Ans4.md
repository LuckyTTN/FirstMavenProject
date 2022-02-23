# FirstMavenProject
Maven Exercise Multi Module Project
Maven is one of the most popular build tools in the Java ecosystem, and one of its core features is dependency management.

Transitive Dependency
There are two types of dependencies in Maven: direct and transitive.

Direct dependencies are the ones that we explicitly include in the project.

These can be included using <dependency> tags
  <dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
</dependency>
On the other hand, direct dependencies require transitive dependencies. Maven automatically includes required transitive dependencies in our project.

We can list all dependencies including transitive dependencies in the project using mvn dependency:tree command.
  Dependency Scopes
Dependency scopes can help to limit transitivity of the dependencies. They also modify the classpath for different build tasks. Maven has six default dependency scopes.

And it's important to understand that each scope — except for import — has an impact on transitive dependencies.
  Compile
This is the default scope when no other scope is provided.
  Dependencies with this scope are available on the classpath of the project in all build tasks. They are also propagated to the dependent projects.

More importantly, these dependencies are also transitive:

<dependency>
    <groupId>commons-lang</groupId>
    <artifactId>commons-lang</artifactId>
    <version>2.6</version>
</dependency>
  Provided
We use this scope to mark dependencies that should be provided at runtime by JDK or a container.

A good use case for this scope would be a web application deployed in some container, where the container already provides some libraries itself. For example, this could be a web server that already provides the Servlet API at runtime.

In our project, we can define those dependencies with the provided scope:
  <dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>servlet-api</artifactId>
    <version>2.5</version>
    <scope>provided</scope>
</dependency>
 The provided dependencies are available only at compile time and in the test classpath of the project. These dependencies are also not transitive.
  Runtime
The dependencies with this scope are required at runtime. But we don't need them for compilation of the project code. Because of that, dependencies marked with the runtime scope will be present in the runtime and test classpath, but they will be missing from the compile classpath.

A JDBC driver is a good example of dependencies that should use the runtime scope:

<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>6.0.6</version>
    <scope>runtime</scope>
</dependency>
  Test
We use this scope to indicate that dependency isn't required at standard runtime of the application but is used only for test purposes.

Test dependencies aren't transitive and are only present for test and execution classpaths.

The standard use case for this scope is adding a test library such as JUnit to our application:

<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>
  
