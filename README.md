# StringDistance

[![Build Status](https://api.travis-ci.org/vickumar1981/stringdistance.svg?branch=master)](https://travis-ci.org/vickumar1981/stringdistance/builds) [![Coverage Status](https://coveralls.io/repos/github/vickumar1981/stringdistance/badge.svg?branch=master)](https://coveralls.io/github/vickumar1981/stringdistance?branch=master) [![Read the Docs](https://img.shields.io/readthedocs/pip.svg)](https://vickumar1981.github.io/stringdistance/api/com/github/vickumar1981/stringdistance/index.html) [![Maven metadata URI](https://img.shields.io/maven-metadata/v/http/central.maven.org/maven2/com/github/vickumar1981/stringdistance_2.12/maven-metadata.xml.svg)](https://mvnrepository.com/artifact/com.github.vickumar1981/stringdistance) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

A fuzzy matching string distance library for Scala and Java that includes Levenshtein distance, Jaro distance, Jaro-Winkler distance, Dice coefficient, N-Gram similarity, Cosine similarity, Jaccard similarity, Longest common subsequence, Hamming distance, and more.

For more detailed information, please refer to the [API Documentation](https://vickumar1981.github.io/stringdistance/api/com/github/vickumar1981/stringdistance/index.html "API Documentation").

Requires: Java 8, 7 or Scala 2.12, 2.11

---
### Contents

1.  [Add it to your project](https://github.com/vickumar1981/stringdistance#add-it-to-your-project-)
2.  [Using in Scala](https://github.com/vickumar1981/stringdistance#scala-usage)
3.  [Using in Scala with implicits](https://github.com/vickumar1981/stringdistance#scala-use-with-implicits)
4.  [Using in Java](https://github.com/vickumar1981/stringdistance#java-usage)
5.  [Adding your own algorithm](https://github.com/vickumar1981/stringdistance#adding-your-own-distance-or-scoring-algorithm)
6.  [Reporting an Issue](https://github.com/vickumar1981/stringdistance#reporting-an-issue)
7.  [License](https://github.com/vickumar1981/stringdistance#license)

---
### Add it to your project ...

__Using sbt:__

In `build.sbt`:
```scala
libraryDependencies += "com.github.vickumar1981" %% "stringdistance" % "1.0.6"
```

__Using gradle:__

In `build.gradle`:
```groovy
dependencies {
    compile 'com.github.vickumar1981:stringdistance_2.12:1.0.6'
}
```

__Using Maven:__

In `pom.xml`:
```xml
<dependency>
    <groupId>com.github.vickumar1981</groupId>
    <artifactId>stringdistance_2.12</artifactId>
    <version>1.0.6</version>
</dependency>
```

Note: For Java 7 or Scala 2.11, please use the `stringdistance_2.11` artifact as a dependency instead.

---
### Scala Usage

__Example.scala__:
```scala
// Scala example
import com.github.vickumar1981.stringdistance.StringDistance._
import com.github.vickumar1981.stringdistance.StringSound._

// Cosine Similarity
val cosSimilarity: Double = Cosine.score("hello", "chello")

// Damerau-Levenshtein Distance
val damerauDist: Int = Damerau.distance("martha", "marhta")
val damerau: Double = Damerau.score("martha", "marhta")

// Dice Coefficient
val diceCoefficient: Double = DiceCoefficient.score("martha", "marhta")

// Hamming Distance
val hammingDist: Int = Hamming.distance("martha", "marhta")
val hamming: Double = Hamming.score("martha", "marhta")

// Jaccard Similarity
val jaccard: Double = Jaccard.score("karolin", "kathrin")

// Jaro and Jaro Winkler
val jaro: Double = Jaro.score("martha", "marhta")
val jaroWinkler: Double = JaroWinkler.score("martha", "marhta")

// Levenshtein Distance
val levenshteinDist: Int = Levenshtein.distance("martha", "marhta")
val levenshtein: Double = Levenshtein.score("martha", "marhta")

// Longest Common Subsequence
val longestCommonSubSeq: Int = LongestCommonSeq.distance("martha", "marhta")

// N-Gram Similarity and Distance
val ngramDist: Int = NGram.distance("karolin", "kathrin")
val bigramDist: Int = NGram.distance("karolin", "kathrin", 2)
val ngramSimilarity: Double = NGram.score("karolin", "kathrin")
val bigramSimilarity: Double = NGram.score("karolin", "kathrin", 2)

// Overlap Similarity
val overlap: Double = Overlap.score("karolin", "kathrin")
val overlapBiGram: Double = Overlap.score("karolin", "kathrin", 2)

// Tversky Similarity
val tversky: Double = Tversky.score("karolin", "kathrin", 0.5)

// Phonetic Similarity
val metaphone: Boolean = Metaphone.score("merci", "mercy")
val soundex: Boolean = Soundex.score("merci", "mercy")
```
---
### Scala: Use with Implicits
  -  To use implicits and extend the String class:  `import com.github.vickumar1981.stringdistance.StringConverter._`

__Example.scala__
```scala
// Scala example using implicits
import com.github.vickumar1981.stringdistance.StringConverter._

// Scores between two strings
val cosSimilarity: Double = "hello".cosine("chello")
val damerau: Double = "martha".damerau("marhta")
val diceCoefficient: Double = "martha".diceCoefficient("marhta")
val hamming: Double = "martha".hamming("marhta")
val jaccard: Double = "karolin".jaccard("kathrin")
val jaro: Double = "martha".jaro("marhta")
val jaroWinkler: Double = "martha".jaroWinkler("marhta")
val levenshtein: Double = "martha".levenshtein("marhta")
val ngramSimilarity: Double = "karolin".nGram("kathrin")
val bigramSimilarity: Double = "karolin".nGram("kathrin", 2)
val overlap: Double = "karolin".overlap("kathrin")
val overlapBiGram: Double "karolin".overlap("kathrin", 2)
val tversky: Double = "karolin".tversky("kathrin", 0.5)

// Distances between two strings
val damerauDist: Int = "martha".damerauDist("marhta")
val hammingDist: Int = "martha".hammingDist("marhta")
val levenshteinDist: Int = "martha".levenshteinDist("marhta")
val longestCommonSeq: Int = "martha".longestCommonSeq("marhta")
val ngramDist: Int = "karolin".nGramDist("kathrin")
val bigramDist: Int = "karolin".nGramDist("kathrin", 2)

// Phonetic similarity of two strings
val metaphone: Boolean = "merci".metaphone("mercy")
val soundex: Boolean = "merci".soundex("mercy")
```
---
### Java Usage
  -  To use in Java:  `import com.github.vickumar1981.stringdistance.util.StringDistance`

__Example.java__
```java
// Java example
import com.github.vickumar1981.stringdistance.util.StringDistance;
import com.github.vickumar1981.stringdistance.util.StringSound;

// Scores between two strings
Double cosSimilarity = StringDistance.cosine("hello", "chello");
Double damerau = StringDistance.damerau("martha", "marhta");
Double diceCoefficient = StringDistance.diceCoefficient("martha", "marhta");
Double hamming = StringDistance.hamming("martha", "marhta");
Double jaccard = StringDistance.jaccard("karolin", "kathrin");
Double jaro = StringDistance.jaro("martha", "marhta");
Double jaroWinkler = StringDistance.jaroWinkler("martha", "marhta");
Double levenshtein = StringDistance.levenshtein("martha", "marhta");
Double ngramSimilarity = StringDistance.nGram("karolin", "kathrin");
Double bigramSimilarity = StringDistance.nGram("karolin", "kathrin", 2);
Double overlap = StringDistance.overlap("karolin", "kathrin");
Double overlapBiGram = StringDistance.overlap("karolin", "kathrin", 2);
Double tversky = StringDistance.tversky("karolin", "kathrin", 0.5);

// Distances between two strings
Integer damerauDist = StringDistance.damerauDist("martha", "marhta");
Integer hammingDist = StringDistance.hammingDist("martha", "marhta");
Integer levenshteinDist = StringDistance.levenshteinDist("martha", "marhta");
Integer longestCommonSeq = StringDistance.longestCommonSeq("martha", "marhta");
Integer ngramDist = StringDistance.nGramDist("karolin", "kathrin");
Integer bigramDist = StringDistance.nGramDist("karolin", "kathrin", 2);

// Phonetic similarity of two strings
Boolean metaphone = StringSound.metaphone("merci", "mercy");
Boolean soundex = StringSound.soundex("merci", "mercy");
```
---

### Adding your own Distance or Scoring Algorithm 

1.  Create a marker trait that extends `StringMetricAlgorithm`:

```scala
trait CustomAlgorithm extends StringMetricAlgorithm
```

2.  Create an implementation for that algorithm using an implicit object.  Override either the `score` or the `distance` method, depending upon whether the object extends `DistanceAlgorithm` or `ScoringAlgorithm`.

```scala
implicit object CustomDistance extends DistanceAlgorithm[CustomAlgorithm] {
    override def distance(s1: String, s2: String): Int = {
        // Implement distance between s1 and s2
    }
}

implicit object CustomScore extends ScoringAlgorithm[CustomAlgorithm] {
    override def score(s1: String, s2: String): Double = {
        // Implement fuzzy score between s1 and s2
    }
}
```

3.  Create an object that extends `StringMetric` using your algorithm as the type parameter, and use the `score` and `distance` methods defined in the implicit object.

```scala
object CustomMetric extends StringMetric[CustomAlgorithm]

val customScore: Double = CustomMetric.score("hello", "hello2")
val customDist: Int = CustomMetric.distance("hello", "hello2")
```
---
### Reporting an Issue

Please report any issues or bugs to the [Github issues page](https://github.com/vickumar1981/stringdistance/issues).

---
### License

This project is licensed under the [Apache 2 License](https://opensource.org/licenses/Apache-2.0).