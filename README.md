# gradle-exclusion-tester
Tester project to verify if gradle correctly honors maven exclusions of dependencies. Logged https://github.com/spring-gradle-plugins/dependency-management-plugin/issues/104 to correct the possible miss in documentation.


	~/github/gradle-exclusion-tester/sample-maven-library> mvn dependency:tree
	[INFO] Scanning for projects...
	[INFO]                                                                         
	[INFO] ------------------------------------------------------------------------
	[INFO] Building sample-maven-lib 1.0.0-SNAPSHOT
	[INFO] ------------------------------------------------------------------------
	[INFO] 
	[INFO] --- maven-dependency-plugin:2.8:tree (default-cli) @ sample-maven-lib ---
	[INFO] com.kilo:sample-maven-lib:jar:1.0.0-SNAPSHOT
	[INFO] \- org.springframework:spring-core:jar:4.2.6.RELEASE:compile
	[INFO] ------------------------------------------------------------------------
	[INFO] BUILD SUCCESS
	[INFO] ------------------------------------------------------------------------
	[INFO] Total time: 0.658 s
	[INFO] Finished at: 2016-08-07T20:46:17-04:00
	[INFO] Final Memory: 29M/1963M
	[INFO] ------------------------------------------------------------------------



	~/gradle-exclusion-tester/sample-maven-app> mvn dependency:tree
	[INFO] Scanning for projects...
	[INFO]                                                                         
	[INFO] ------------------------------------------------------------------------
	[INFO] Building sample-maven-app 1.0.0-SNAPSHOT
	[INFO] ------------------------------------------------------------------------
	[INFO] 
	[INFO] --- maven-dependency-plugin:2.8:tree (default-cli) @ sample-maven-app ---
	[INFO] com.kilo:sample-maven-app:jar:1.0.0-SNAPSHOT
	[INFO] +- org.springframework:spring-beans:jar:4.2.6.RELEASE:compile
	[INFO] |  \- org.springframework:spring-core:jar:4.2.6.RELEASE:compile
	[INFO] |     \- commons-logging:commons-logging:jar:1.2:compile
	[INFO] \- com.kilo:sample-maven-lib:jar:1.0.0-SNAPSHOT:compile
	[INFO] ------------------------------------------------------------------------
	[INFO] BUILD SUCCESS
	[INFO] ------------------------------------------------------------------------
	[INFO] Total time: 0.646 s
	[INFO] Finished at: 2016-08-07T20:48:45-04:00
	[INFO] Final Memory: 27M/1963M
	[INFO] ------------------------------------------------------------------------



	~/gradle-exclusion-tester/sample-gradle-app> ./gradlew  dependencies --configuration compile
	:dependencies

	------------------------------------------------------------
	Root project
	------------------------------------------------------------

	compile - Dependencies for source set 'main'.
	+--- org.springframework:spring-beans:4.2.6.RELEASE
	|    \--- org.springframework:spring-core:4.2.6.RELEASE
	|         \--- commons-logging:commons-logging:1.2
	\--- com.kilo:sample-maven-lib:1.0.0-SNAPSHOT
		 \--- org.springframework:spring-core:4.2.6.RELEASE (*)

	(*) - dependencies omitted (listed previously)

	BUILD SUCCESSFUL

	Total time: 2.264 secs
