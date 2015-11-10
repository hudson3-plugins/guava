# guava
Forked guava 14.0.1 to address undeploy memory leaks

For some reason, the gpg plugin isn't doing it's job of signing files as part of the
normal release process. Therefore, after doing prepare and release, the sonatype
repository will be missing all .asc files, and you need to run the following to fix it.

    #deploy asc files for guava (why doesn't this Just Work?)
    mvn gpg:sign-and-deploy-file -Durl=http://oss.sonatype.org/service/local/staging/deploy/maven2 -DrepositoryId=sonatype-nexus-staging -DgroupId=org.hudsonci.lib.guava -DartifactId=guava -Dversion=14.0.1-h-3 -DgeneratePom=false -Dclassifier=javadoc -Dfile=target/guava-14.0.1-h-3-javadoc.jar
    mvn gpg:sign-and-deploy-file -Durl=http://oss.sonatype.org/service/local/staging/deploy/maven2 -DrepositoryId=sonatype-nexus-staging -DgroupId=org.hudsonci.lib.guava -DartifactId=guava -Dversion=14.0.1-h-3 -DgeneratePom=false -Dclassifier=sources -Dfile=target/guava-14.0.1-h-3-sources.jar
    # NOTE: Must restore released pom.xml (with correct non-SNAPSHOT version) or save it as X and change -DpomFile=X before running this!
    mvn gpg:sign-and-deploy-file -Durl=http://oss.sonatype.org/service/local/staging/deploy/maven2 -DrepositoryId=sonatype-nexus-staging -DgroupId=org.hudsonci.lib.guava -DartifactId=guava -Dversion=14.0.1-h-3 -DpomFile=pom.xml -Dfile=target/guava-14.0.1-h-3.jar
