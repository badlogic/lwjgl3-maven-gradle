# LWJGL 3 Maven/Gradle sample
This sample demonstrates how to use LWJGL 3 via Maven or Gradle. The `pom.xml` and `build.gradle` files show you the general setup when using LWJGL 3 with either build system.


## Maven
To use LWJGL 3 via Maven, add the following dependencies to your `pom.xml`:

```xml
<properties>
	<lwjgl.version>3.0.0a</lwjgl.version>
</properties>

<dependencies>
	<dependency>
		<groupId>org.lwjgl</groupId>
		<artifactId>lwjgl</artifactId>
		<version>${lwjgl.version}</version>
	</dependency>
	<dependency>
		<groupId>org.lwjgl</groupId>
		<artifactId>lwjgl-platform</artifactId>
		<version>${lwjgl.version}</version>
		<classifier>natives-windows</classifier>
	</dependency>
	<dependency>
		<groupId>org.lwjgl</groupId>
		<artifactId>lwjgl-platform</artifactId>
		<version>${lwjgl.version}</version>
		<classifier>natives-osx</classifier>
	</dependency>
	<dependency>
		<groupId>org.lwjgl</groupId>
		<artifactId>lwjgl-platform</artifactId>
		<version>${lwjgl.version}</version>
		<classifier>natives-linux</classifier>
	</dependency>
</dependencies>

```

Note the `<properties>` element, which lets you easily switch between versions of LWJGL. The `lwjgl` artifact contains the core API of LWJGL. The `lwjgl-platform` artifacts each contain the native shared libraries for the platforms Windows, Linux and Mac OS X. You can remove dependencies for platforms you don't want to support, or you can modify your build to generate platform specific distributions, only containing the shared libraries required for each platform.

LWJGL also releases snapshot builds daily to SonaType. This lets you use the latest and greatest changes from the [Git master branch](https://github.com/LWJGL/lwjgl3). To use a snapshot build, you need to add the SonaType snapshot repository to your `pom.xml`:

```xml
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

Then simply change the `<lwjgl.version>` element to a snapshot version, e.g. `3.0.0a-SNAPSHOT`.

## Gradle
To use LWJGL 3 via Gradle, add the following dependencies to your `build.gradle`:

```gradle
project.ext.lwjglVersion = "3.0.0a"

dependencies {
	compile "org.lwjgl:lwjgl:${lwjglVersion}"
	compile "org.lwjgl:lwjgl-platform:${lwjglVersion}:natives-windows"
	compile "org.lwjgl:lwjgl-platform:${lwjglVersion}:natives-linux"
	compile "org.lwjgl:lwjgl-platform:${lwjglVersion}:natives-osx"
}
```

Note the assignment to `project.ext.lwjglVersion`, which lets you easily switch between versions of LWJGL. The `lwjgl` artifact contains the core API of LWJGL. The `lwjgl-platform` artifacts each contain the native shared libraries for the platforms Windows, Linux and Mac OS X. You can remove dependencies for platforms you don't want to support, or you can modify your build to generate platform specific distributions, only containing the shared libraries required for each platform.

LWJGL also releases snapshot builds daily to SonaType. This lets you use the latest and greatest changes from the [Git master branch](https://github.com/LWJGL/lwjgl3). To use a snapshot build, you need to add the SonaType snapshot repository to your `build.gradle:

```gradle
repositories {
    mavenCentral()
    maven { url "https://oss.sonatype.org/content/repositories/snapshots/" }
}
```

Then simply assign a snapshot version to `project.ext.lwjglVersion`, e.g. `3.0.0a-SNAPSHOT`.

## Shared library loading
The source of this repository contains a class `SharedLibraryLoader`. It lets you load the platform specific shared library from the platform JARs pulled in as dependencies. Before accessing any LWJGL APIs, simply call:

```java
SharedLibraryLoader.load()
```

You can do this as the first statement in your application's `main` method.
