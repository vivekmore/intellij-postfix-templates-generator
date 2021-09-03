# Template File Generator for Custom Postfix Templates
This tool simplifies and automates the generation of [Custom Postfix Templates](https://github.com/xylo/intellij-postfix-templates) for Intellij IDEA.  It scans utility classes and generates postfix templates for its static methods.

## Background

### Task

We would like to extend an existing type with a new method, e.g.
```java
String.isNumeric
```

### Workaround

Since Java does not allow libraries to extend existing types the common solution is to write a utility class containing the new method which takes as first parameter the source object (and maybe additional method arguments), e.g.
```java
public class StringUtils {
    public static boolean isNumeric(String s) {...}
}
```

However, to apply this function to your string object you need to be aware of the existence of this function and you need to know in which utility class it is located.  This is combersome and unintuitive.

### Solution: Postfix Template

Using the [Custom Postfix Templates](https://github.com/xylo/intellij-postfix-templates) plugin of Intellij IDEA we can actually define postfix templates that allow us to write
```java
"foo".isNumeric
```

and expand this expression to
```java
StringUtils.isNumeric("foo")
```

### Automatic Template File Generation

Instead of writing all postfix templates by hand this tool can automate most of this process for you.
Just add your library as dependency to the `pom.xml`.
Then open the Scala file `PostfixTemplateGenerator` and add your `UtilsCollection` configuration to the list `utilsCollections`.
Finally, run `PostfixTemplateGenerator` and your templates file will be generated for Java and Scala.
