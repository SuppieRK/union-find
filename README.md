# Hash Set with Union Find capabilities

This dependency-less library serves for one simple purpose: provide an implementation of a data structure with Union-Find algorithm capabilities.

[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2FSuppieRK%2Funion-find.svg?type=shield&issueType=license)](https://app.fossa.com/projects/git%2Bgithub.com%2FSuppieRK%2Funion-find?ref=badge_shield&issueType=license)

[![SonarCloud](https://sonarcloud.io/images/project_badges/sonarcloud-orange.svg)](https://sonarcloud.io/summary/overall?id=SuppieRK_union-find)

## Where can this be useful?

Union-Find algorithm is a good fit for tasks which require to:
- Join elements together to form a union.
- See if two elements belong to the same set.

Some of the practical applications are:
- Games (Go, Hex).
- Dynamic connectivity problems (Kruskal's minimum spanning tree algorithm, graph cycle detection).
- Image processing (segment an image based on its pixel qualities).
- Social network analysis (finding clusters / communities in social networks).

## How to use

```java
public class Example {
  public static void main(String[] args) {
    HashUnionFindSet<Character, String> hufs =
        // Note the function - it defines initial disjoint set for the value
        // Function itself cannot be null, as well as its return value
        new HashUnionFindSet<>(s -> Character.toLowerCase(s.charAt(0)));

    // Let's define our fruits
    final String apple = "Apple";
    final String banana = "Banana";
    final String apricot = "Apricot";
    final String blueberry = "Blueberry";

    // The first two fruits will be in different sets
    hufs.add(apple);
    hufs.add(banana);
    System.out.printf(
        "Are %s and %s connected? - %s%n", 
        apple, banana, hufs.connected(apple, banana));

    // Apricot will join the same set as Apple
    hufs.add(apricot);
    System.out.printf(
        "Are %s and %s connected? - %s%n", 
        apple, apricot, hufs.connected(apple, apricot));

    // Let's check our state
    System.out.println();
    System.out.printf(
        "There are %s disjoint sets%n", 
        hufs.numberOfSets());
    System.out.printf(
        "%s and %s belong to the set '%s' of size %s%n",
        apple, apricot, hufs.find(apple), hufs.elementSetSize(apple));
    System.out.printf(
        "%s belongs to the set '%s' of size %s%n",
        banana, hufs.find(banana), hufs.elementSetSize(banana));

    // Let's join our sets
    hufs.union(apple, banana);

    // And check our state again
    System.out.println();
    System.out.printf(
        "After union there is %s disjoint set%n", 
        hufs.numberOfSets());
    System.out.printf(
        "%s and %s belong to the set '%s' of size %s%n",
        apple, apricot, hufs.find(apple), hufs.elementSetSize(apple));
    System.out.printf(
        "And %s belongs to the same set '%s' of size %s now%n",
        banana, hufs.find(banana), hufs.elementSetSize(banana));
    System.out.printf(
        "Is the set under letter 'b' still present? - %s%n", 
        hufs.hasRepresentative('b'));

    // Let's throw in another fruit
    hufs.add(blueberry);

    // And check our state for the last time
    System.out.println();
    System.out.printf(
        "There are %s disjoint sets now%n", 
        hufs.numberOfSets());
    System.out.printf(
        "%s, %s and %s still belong to the set '%s' of size %s%n",
        apple, apricot, banana, hufs.find(apple), hufs.elementSetSize(apple));
    System.out.printf(
        "But %s belongs to the set '%s' of size %s%n",
        blueberry, hufs.find(blueberry), hufs.elementSetSize(blueberry));
  }
}
```

which will produce the following output:

```
Are Apple and Banana connected? - false
Are Apple and Apricot connected? - true

There are 2 disjoint sets
Apple and Apricot belong to the set 'a' of size 2
Banana belongs to the set 'b' of size 1

After union there is 1 disjoint set
Apple and Apricot belong to the set 'a' of size 3
And Banana belongs to the same set 'a' of size 3 now
Is the set under letter 'b' still present? - false

There are 2 disjoint sets now
Apple, Apricot and Banana still belong to the set 'a' of size 3
But Blueberry belongs to the set 'b' of size 1
```

## How to add

- Maven
```xml
<dependency>
    <groupId>io.github.suppierk</groupId>
    <artifactId>union-find</artifactId>
    <version>1.1.0</version>
</dependency>
```

- Gradle
```groovy
implementation 'io.github.suppierk:union-find:1.1.0'
```

## Useful reading

- [Union−Find Applications | Welcome to Algorithms | edX Series](https://youtu.be/OMxd43qB6Bg?si=ZnWuIOWQPMLafTwh)
- [Union-Find with Constant Time Deletions](https://www.cs.princeton.edu/courses/archive/fall05/cos528/handouts/Union-Find%20with%20Constant%20Time%20Deletions.pdf)
- [Union-Find with deletions](http://www.aladdin.cs.cmu.edu/papers/pdfs/y2003/uniof.pdf)
- [A simple and efficient Union-Find-Delete algorithm](https://www.sciencedirect.com/science/article/pii/S030439751000616X?ref=pdf_download&fr=RR-9&rr=86db096b1f70152a)

## Inspired by

- [JGraphT implementation](https://github.com/jgrapht/jgrapht/blob/master/jgrapht-core/src/main/java/org/jgrapht/alg/util/UnionFind.java)
- [Partition implementation](https://github.com/gstamatelat/partition/blob/master/src/main/java/gr/james/partition/UnionFindPartition.java)

## FOSSA report

[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2FSuppieRK%2Funion-find.svg?type=large&issueType=license)](https://app.fossa.com/projects/git%2Bgithub.com%2FSuppieRK%2Funion-find?ref=badge_large&issueType=license)
