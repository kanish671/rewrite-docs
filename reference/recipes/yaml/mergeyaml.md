# Merge YAML snippet

** org.openrewrite.yaml.MergeYaml**
_Merge a YAML snippet with an existing YAML document._

## Source

[Github](https://github.com/openrewrite/rewrite), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://search.maven.org/artifact/org.openrewrite/rewrite-yaml/7.8.1/jar)

* groupId: org.openrewrite
* artifactId: rewrite-yaml
* version: 7.8.1

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | key | XPath expression used to find matching keys. |
| `String` | yaml | The YAML snippet to insert. The snippet will be indented to match the style of its surroundings. |


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your rewrite.yml create a new recipe with a unique name. For example: `com.yourorg.MergeYamlExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.MergeYamlExample
displayName: Merge YAML snippet example
recipeList:
  - org.openrewrite.yaml.MergeYaml:
      key: /metadata
      yaml: labels: 
	label-one: "value-one"
```
{% endcode %}


Now that `com.yourorg.MergeYamlExample` has been defined activate it in your build file:

{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("5.2.1")
}

rewrite {
    activeRecipe("com.yourorg.MergeYamlExample")
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
        <version>4.6.2</version>
        <configuration>
          <activeRecipes>
            <recipe>com.yourorg.MergeYamlExample</recipe>
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

Recipes can also be activated directly from the commandline by adding the argument `-DactiveRecipe=com.yourorg.MergeYamlExample`