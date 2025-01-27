[![MIT Licensed](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/meraki-analytics/orianna/blob/master/LICENSE.txt)
[![Maven Central](https://img.shields.io/maven-central/v/com.merakianalytics.orianna/orianna.svg)](https://search.maven.org/search?q=g:com.merakianalytics.orianna)
[![Documentation Status](https://readthedocs.org/projects/orianna/badge/)](http://orianna.readthedocs.org/en/latest/)
[![JavaDocs](http://javadoc.io/badge/com.merakianalytics.orianna/orianna.svg)](http://javadoc.io/doc/com.merakianalytics.orianna/orianna)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.1169620.svg)](https://doi.org/10.5281/zenodo.1169620)

# Orianna
A Java adaptation of the Riot Games League of Legends API (https://developer.riotgames.com/).

Orianna is the sister library to [Cassiopeia](https://github.com/meraki-analytics/cassiopeia) (Python). It's been designed with usability in mind - making sure all the bookkeeping is done right so you can focus on getting the data you need and building your application.

Orianna is licensed under the [MIT License](https://github.com/meraki-analytics/orianna/blob/master/LICENSE.txt).

## Documentation & Examples
Detailed documentation about Orianna is located [here](http://orianna.readthedocs.io/en/latest/). The full JavaDoc for Orianna is available [here](http://javadoc.io/doc/com.merakianalytics.orianna/orianna). Examples of using Orianna can be found [here](https://github.com/meraki-analytics/orianna/tree/master/orianna-examples/src/main/java/com/merakianalytics/orianna/examples).

## Features
Orianna is designed to make the lives of Riot API developers as easy as possible. Here are some of the ways we do it:
- An enhanced user interface that makes using the Riot API easy and fun
  - Restructured and renamed API data for maximum clarity
  - Fluent APIs for requesting data
  - Automatic conversion of foreign keys into the objects they specify (e.g player.getChampion() instead of player.getChampionId())
- Rate limits handled automatically with optimal usage of your API key
- Configurable handling of API errors (e.g. automatic retry on 500 errors)
- Built-in automatic caching, ready out of the box
- DataDragon support
- A highly configurable [pipeline](https://github.com/meraki-analytics/datapipelines-java) for requesting and caching Riot API data
  - Allows flexibility in what database(s) you want to use to cache your data
  - Off-the-shelf support for many popular databases under construction [here](https://github.com/meraki-analytics/orianna-datastores)
  - Extensible to seamlessly integrate other data types and APIs, such as the [ChampionGG API](http://api.champion.gg/) (ChampionGG support coming soon!)

## How to get it
Orianna is distributed through the [releases page](https://github.com/meraki-analytics/orianna/releases) and through [Maven Central](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.merakianalytics.orianna%22). The easiest way to get it is by using [Maven](https://maven.apache.org/) or [Gradle](https://gradle.org/).

### Maven
To add the latest Orianna release version to your maven project, add the dependency to your `pom.xml` dependencies section:
```xml
<dependencies>
  <dependency>
    <groupId>com.merakianalytics.orianna</groupId>
    <artifactId>orianna</artifactId>
    <version>4.0.0-rc3</version>
    <!-- or, for Android: -->
    <artifactId>orianna-android</artifactId>
    <version>4.0.0-rc3</version>
  </dependency>
</dependencies>
```
Or, if you want to get the latest development version, add the [Sonaype Snapshot Repository](https://oss.sonatype.org/content/repositories/snapshots/) to your `pom.xml` as well:
```xml
<dependencies>
  <dependency>
    <groupId>com.merakianalytics.orianna</groupId>
    <artifactId>orianna</artifactId>
    <version>4.0.0-SNAPSHOT</version>
    <!-- or, for Android: -->
    <artifactId>orianna-android</artifactId>
    <version>4.0.0-SNAPSHOT</version>
  </dependency>
</dependencies>

<repositories>
  <repository>
    <id>snapshots-repo</id>
    <url>https://oss.sonatype.org/content/repositories/snapshots</url>
    <releases>
      <enabled>false</enabled>
    </releases>
    <snapshots>
      <enabled>true</enabled>
    </snapshots>
  </repository>
</repositories>
```

### Gradle
To add the latest Orianna release version to your gradle project, add the [Maven Central](https://search.maven.org/) repository to your `build.gradle` repositories section, and add the dependency to your build.gradle dependencies section:
```gradle
repositories {
  mavenCentral()
}

dependencies {
  implementation "com.merakianalytics.orianna:orianna:4.0.0-rc3"
  // or, for Android:
  implementation "com.merakianalytics.orianna:orianna-android:4.0.0-rc3"
}
```
Or, if you want to get the latest development version, add the [Sonaype Snapshot Repository](https://oss.sonatype.org/content/repositories/snapshots/) to your `build.gradle` instead:
```gradle
repositories {
  maven { url "https://oss.sonatype.org/content/repositories/snapshots" }
}

dependencies {
  implementation "com.merakianalytics.orianna:orianna:4.0.0-SNAPSHOT"
  // or, for Android:
  implementation "com.merakianalytics.orianna:orianna-android:4.0.0-SNAPSHOT"
}
```

### Using the release JAR directly
Grab the latest JAR from the [releases page](https://github.com/meraki-analytics/orianna/releases) and add it to your project dependencies. JARs are provide both with and without Orianna's dependencies included. The `jar-with-dependencies` version will get you up & running faster, but can cause version conflicts if your project has other dependencies.

If you're using the JAR without dependencies inlcuded, Orianna depends on the following libraries which will also need to be added as dependencies:
- [slf4j-api](https://www.slf4j.org/) (version 1.7.25)
- [datapipelines](https://github.com/meraki-analytics/datapipelines-java) (version 1.0.4)
- [hipster4j](http://www.hipster4j.org/) (version 1.0.1)
- [guava](https://github.com/google/guava) (version 20.0)
- [okhttp](http://square.github.io/okhttp/) (version 3.12.1)
- [jackson-databind](https://github.com/FasterXML/jackson-databind) (version 2.9.8)
- [jackson-dataformat-msgpack](https://github.com/msgpack/msgpack-java) (version 0.8.16)
- [joda-time](http://www.joda.org/joda-time/) (version 2.10.1)
- [jackson-datatype-joda](https://github.com/FasterXML/jackson-datatype-joda) (version 2.9.8)
- [cache2k](https://cache2k.org/) (version 1.2.0.Final)

## Example
Check out a basic example of Orianna in action. More examples are available [here](https://github.com/meraki-analytics/orianna/tree/master/orianna-examples/src/main/java/com/merakianalytics/orianna/examples).
```java
import com.merakianalytics.orianna.Orianna;
import com.merakianalytics.orianna.types.common.Queue;
import com.merakianalytics.orianna.types.common.Region;
import com.merakianalytics.orianna.types.core.league.League;
import com.merakianalytics.orianna.types.core.staticdata.Champion;
import com.merakianalytics.orianna.types.core.staticdata.Champions;
import com.merakianalytics.orianna.types.core.summoner.Summoner;

public class Example {
    public static void main(String[] args) {
        Orianna.setRiotAPIKey("YOUR-API-KEY");
        Orianna.setDefaultRegion(Region.NORTH_AMERICA);

        Summoner summoner = Orianna.summonerNamed("FatalElement").get();
        System.out.println(summoner.getName() + " is level " + summoner.getLevel() + " on the " + summoner.getRegion() + " server.");

        Champions champions = Orianna.getChampions();
        Champion randomChampion = champions.get((int)(Math.random() * champions.size()));
        System.out.println("He enjoys playing champions such as " + randomChampion.getName());

        League challengerLeague = Orianna.challengerLeagueInQueue(Queue.RANKED_SOLO_5x5).get();
        Summoner bestNA = challengerLeague.get(0).getSummoner();
        System.out.println("He's not as good as " + bestNA.getName() + " at League, but probably a better Java programmer!");
    }
}
```

## Configuring Orianna
Orianna ships with a [default configuration](https://github.com/meraki-analytics/orianna/blob/master/orianna/src/main/resources/com/merakianalytics/orianna/default-orianna-config.json) designed to get new users going as quickly as possible. However, you may find you want to take advantage of some of the configuration options Orianna supports by replacing that configuration with your own.

Orianna is able to automatically load your Riot API Key from your environment variables on startup. To take advantage of this, set your `RIOT_API_KEY` environment variable to your Riot API Key.

For more complex configuration, just download the [default configuration](https://github.com/meraki-analytics/orianna/blob/master/orianna/src/main/resources/com/merakianalytics/orianna/default-orianna-config.json), make the changes you'd like, and load the new configuration file when your program starts. Documentation describing the full range of configuration options available with Orianna can be found [here](http://orianna.readthedocs.io/en/latest/configuring-orianna.html).
```java
Orianna.loadConfiguration(new File("/path/to/your/configuration-file.json"));
```
Alternatively, Orianna can automatically load your configuration file on startup if you set your `ORIANNA_CONFIGURATION_PATH` environment variable to the path of your configuration file.

## Android Usage Note
If you're using Orianna with Android, be aware that using the default configuration which uses the [RiotAPI Data Source](https://github.com/meraki-analytics/orianna/blob/master/orianna/src/main/java/com/merakianalytics/orianna/datapipeline/riotapi/RiotAPI.java) will result in leaking your API key to the users of your application as they can access the program memory and network requests Orianna is making. For personal applications you won't be sharing, that's okay. If you're going to distribute your application, however, you'll need to have Orianna make its calls indirectly through a proxy server. You can use [Kernel](https://github.com/meraki-analytics/kernel) to easily set up a proxy server along with the [Kernel Data Source](https://github.com/meraki-analytics/orianna/blob/master/orianna/src/main/java/com/merakianalytics/orianna/datapipeline/kernel/dto/Kernel.java) in Orianna to send your requests to it instead of the Riot API. 

### Simple Kernel Configuration
[Here's an example](https://gist.github.com/robrua/c9248aa80212849e95e9002fac1970eb) of an Orianna configuration file that uses Kernel instead of the Riot API. Specifically, note [this section](https://gist.github.com/robrua/c9248aa80212849e95e9002fac1970eb#file-orianna-config-json-L201-L271) which replaces [this section](https://github.com/meraki-analytics/orianna/blob/master/orianna-android/src/main/resources/com/merakianalytics/orianna/default-orianna-config.json#L201-L276) from the default configuration.

### Recommended Kernel Configuration
It's recommended to configure Kernel to send "data" layer Orianna objects, rather than the "dto" layer objects it sends by default which mirror the Riot API exactly. This will reduce the amount of repeated computation that needs to be done between the Kernel server and the client Orianna instance. To use the "data" layer, configure your Kernel instance to "produceCoreData", as shown [here](https://github.com/meraki-analytics/kernel/blob/master/configurations/data/base/kernel-config.json#L2). On the Orianna end, you can then replace the Riot API configuration from the default configuration (shown [here](https://github.com/meraki-analytics/orianna/blob/master/orianna-android/src/main/resources/com/merakianalytics/orianna/default-orianna-config.json#L201-L276)) with the "data" layer Kernel data source as shown [here](https://gist.github.com/robrua/cd9a1a082f2069750d2dbded11f5c770#file-orianna-config-json-L201-L271). You can also remove most of the [transformers](https://github.com/meraki-analytics/orianna/blob/master/orianna-android/src/main/resources/com/merakianalytics/orianna/default-orianna-config.json#L279-L297) from the default configuration (shown [here](https://gist.github.com/robrua/cd9a1a082f2069750d2dbded11f5c770#file-orianna-config-json-L274-L276)) as they won't be needed.

## Questions & Contributions
Feel free to send pull requests or to contact us via GitHub or [Discord](https://discord.gg/JRDk2JU). We also hang around the [Riot API Discord](https://discord.gg/riotapi), so come by and say hello. We love to hear what people are building with Orianna! If you would like to help us maintain Orianna, let us know on our [Discord](https://discord.gg/JRDk2JU).

## Bugs
If you find bugs please let us know via a pull request or issue.

## Citing Orianna
If you used Orianna for your research, please [cite the project](https://doi.org/10.5281/zenodo.1169620).

## Support Us
If you've loved using Orianna, consider supporting us through [PayPal](https://www.paypal.me/merakianalytics) or [Patreon](https://www.patreon.com/merakianalytics).

## Disclaimer
Orianna isn't endorsed by Riot Games and doesn't reflect the views or opinions of Riot Games or anyone officially involved in producing or managing League of Legends. League of Legends and Riot Games are trademarks or registered trademarks of Riot Games, Inc. League of Legends © Riot Games, Inc.
