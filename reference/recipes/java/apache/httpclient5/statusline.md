# Migrate to ApacheHttpClient 5.x deprecated methods from 4.x

**org.openrewrite.java.apache.httpclient5.StatusLine**

_Migrates deprecated methods to their equivalent ones in 5.x_

## Source

[GitHub](https://github.com/openrewrite/rewrite-spring/blob/main/src/main/resources/META-INF/rewrite/apache-httpclient-5.yml), [Issue Tracker](https://github.com/openrewrite/rewrite-spring/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-spring/5.0.7/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-spring
* version: 5.0.7


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-spring:5.0.7` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.24")
}

rewrite {
    activeRecipe("org.openrewrite.java.apache.httpclient5.StatusLine")
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
{% tab title="Maven POM" %}
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
            <recipe>org.openrewrite.java.apache.httpclient5.StatusLine</recipe>
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

{% tab title="Maven Command Line" %}
{% code title="shell" %}
You will need to have [Maven](https://maven.apache.org/download.cgi) installed on your machine before you can run the following command.

```shell
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run \
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-spring:RELEASE \
  -Drewrite.activeRecipes=org.openrewrite.java.apache.httpclient5.StatusLine
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Simplify a call chain](../../../java/simplifymethodchain.md)
  * methodPatternChain: `[org.apache.hc.core5.http.HttpResponse getStatusLine(), org.apache.hc.core5.http.message.StatusLine getStatusCode()]`
  * newMethodName: `getCode`
* [Simplify a call chain](../../../java/simplifymethodchain.md)
  * methodPatternChain: `[org.apache.hc.core5.http.HttpResponse getStatusLine(), org.apache.hc.core5.http.message.StatusLine getReasonPhrase()]`
  * newMethodName: `getReasonPhrase`
* [Simplify a call chain](../../../java/simplifymethodchain.md)
  * methodPatternChain: `[org.apache.hc.core5.http.HttpResponse getStatusLine(), org.apache.hc.core5.http.message.StatusLine getProtocolVersion()]`
  * newMethodName: `getVersion`
* [Replaces deprecated `HttpResponse::getStatusLine()`](../../../java/apache/httpclient5/newstatusline.md)

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.apache.httpclient5.StatusLine
displayName: Migrate to ApacheHttpClient 5.x deprecated methods from 4.x
description: Migrates deprecated methods to their equivalent ones in 5.x
recipeList:
  - org.openrewrite.java.SimplifyMethodChain:
      methodPatternChain: [org.apache.hc.core5.http.HttpResponse getStatusLine(), org.apache.hc.core5.http.message.StatusLine getStatusCode()]
      newMethodName: getCode
  - org.openrewrite.java.SimplifyMethodChain:
      methodPatternChain: [org.apache.hc.core5.http.HttpResponse getStatusLine(), org.apache.hc.core5.http.message.StatusLine getReasonPhrase()]
      newMethodName: getReasonPhrase
  - org.openrewrite.java.SimplifyMethodChain:
      methodPatternChain: [org.apache.hc.core5.http.HttpResponse getStatusLine(), org.apache.hc.core5.http.message.StatusLine getProtocolVersion()]
      newMethodName: getVersion
  - org.openrewrite.java.apache.httpclient5.NewStatusLine

```
{% endtab %}
{% endtabs %}

## Contributors
* [Joan Viladrosa](mailto:joan@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.apache.httpclient5.StatusLine)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.