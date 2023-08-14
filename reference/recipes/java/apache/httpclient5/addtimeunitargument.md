# Adds a TimeUnit argument to the matched method invocations

**org.openrewrite.java.apache.httpclient5.AddTimeUnitArgument**

_In Apache Http Client 5.x migration, an extra TimeUnit argument is required in the timeout and duration methods. Previously in 4.x, all these methods were implicitly having the timeout or duration expressed in milliseconds, but in 5.x the unit of the timeout or duration is required. So, by default this recipe adds `TimeUnit.MILLISECONDS`, it is possible to specify this as a parameter. Since all affected methods of the Apache Http Client 5.x migration only have one integer/long argument, the recipe applies with matched method invocations of exactly one parameter._

## Source

[GitHub](https://github.com/openrewrite/rewrite-spring/blob/main/src/main/java/org/openrewrite/java/apache/httpclient5/AddTimeUnitArgument.java), [Issue Tracker](https://github.com/openrewrite/rewrite-spring/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-spring/5.0.7/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-spring
* version: 5.0.7

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | methodPattern | A [method pattern](/reference/method-patterns.md) that is used to find matching method invocations. |
| `TimeUnit` | timeUnit | *Optional*. The TimeUnit enum value we want to add to the method invocation. Defaults to `MILLISECONDS`. |


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.AddTimeUnitArgumentExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.AddTimeUnitArgumentExample
displayName: Adds a TimeUnit argument to the matched method invocations example
recipeList:
  - org.openrewrite.java.apache.httpclient5.AddTimeUnitArgument:
      methodPattern: org.apache.http.client.config.RequestConfig.Builder setConnectionRequestTimeout(int)
      timeUnit: MILLISECONDS
```
{% endcode %}

Now that `com.yourorg.AddTimeUnitArgumentExample` has been defined activate it and take a dependency on org.openrewrite.recipe:rewrite-spring:5.0.7 in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.24")
}

rewrite {
    activeRecipe("com.yourorg.AddTimeUnitArgumentExample")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-spring:5.0.7")
}
```
{% endcode %}
{% endtab %}
{% tab title="Maven" %}
{% code title="pom.xml" %}
```markup
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.openrewrite.maven</groupId>
        <artifactId>rewrite-maven-plugin</artifactId>
        <version>5.4.1</version>
        <configuration>
          <activeRecipes>
            <recipe>com.yourorg.AddTimeUnitArgumentExample</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-spring</artifactId>
            <version>5.0.7</version>
          </dependency>
        </dependencies>
      </plugin>
    </plugins>
  </build>
</project>
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [joanvr](mailto:joan@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.apache.httpclient5.AddTimeUnitArgument)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.