# Remove exclusion

** org.openrewrite.maven.RemoveExclusion**
_Remove a single exclusion from on a particular dependency._

## Source

[Github](https://github.com/openrewrite/rewrite), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://search.maven.org/artifact/org.openrewrite/rewrite-maven/7.16.0/jar)

* groupId: org.openrewrite
* artifactId: rewrite-maven
* version: 7.16.0

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | groupId | The first part of a dependency coordinate 'com.google.guava:guava:VERSION'. |
| `String` | artifactId | The second part of a dependency coordinate 'com.google.guava:guava:VERSION'. |
| `String` | exclusionGroupId | The first part of a dependency coordinate 'com.google.guava:guava:VERSION'. |
| `String` | exclusionArtifactId | The second part of a dependency coordinate 'com.google.guava:guava:VERSION'. |


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your rewrite.yml create a new recipe with a unique name. For example: `com.yourorg.RemoveExclusionExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.RemoveExclusionExample
displayName: Remove exclusion example
recipeList:
  - org.openrewrite.maven.RemoveExclusion:
      groupId: com.google.guava
      artifactId: guava
      exclusionGroupId: com.google.guava
      exclusionArtifactId: guava
```
{% endcode %}


Now that `com.yourorg.RemoveExclusionExample` has been defined activate it in your build file:

{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("5.14.0")
}

rewrite {
    activeRecipe("com.yourorg.RemoveExclusionExample")
}

repositories {
    mavenCentral()
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
        <version>4.16.0</version>
        <configuration>
          <activeRecipes>
            <recipe>com.yourorg.RemoveExclusionExample</recipe>
          </activeRecipes>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```
{% endcode %}
{% endtab %}
{% endtabs %}

Recipes can also be activated directly from the commandline by adding the argument `-DactiveRecipe=com.yourorg.RemoveExclusionExample`