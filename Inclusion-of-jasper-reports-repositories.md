# Inclusion of the Jasper Reports Repositories

**Question:** Why is it that during the build the project fails to 
download com.lowagie:itext:jar:2.1.7.js6?

Simple. The above dependency does not exist. The strange decision by
jasper reports not use the main stream com.lowagie:itext:jar:2.1.7 and instead use com.lowagie:itext:jar:2.1.7.js6 posted in a non-usual
maven repository, means that local builds are doomed to fail.
<br>
What makes matters worse, is that, you could actually package a local build with you maven, yet, it will not contain that artefact since it is not open declared in the pom for dynamic reports.
<br>
But if the user is going to generate PDF files at runtime, the program simply crashes

## Fixing it
To fix the above problem is a matter of cloning the jasper reports library and change their pom then deploying a personal copy. 
But the most likely way to fix it is to simply include the repository in the pom of the dynamic reports. This means we include the following line:
```xml
    <repositories>
        <!--Repository containing com.lowagie:itext:jar:2.1.7.js6, not available in maven central-->
        <repository>
            <id>jaspersoft-third-party</id>
            <url>
                http://jaspersoft.jfrog.io/jaspersoft/third-party-ce-artifacts/
            </url>
        </repository>
        <repository>
            <id>jr-ce-releases</id>
            <name>JasperReports CE Releases</name>
            <url>
                http://jaspersoft.jfrog.io/jaspersoft/jr-ce-releases
            </url>
        </repository>
    </repositories>
```

## Arguments For
- We won't have to maintain jasper reports ourselves
- We can always, at a later date deploy the same artefact from our own 'github' repository

## Arguments Against
- Using this repos, leads to warnings being generated especially when generating project reports
- We don't know yet whether by renaming the library, whether the 
publisher implies that this is now a non-public artefact

## Decision
- For now we are using the repositories, but are open to suggestions. This has gone a long way in making the build stable which is one of our desparate and need-to-fix-fast goals.

TBD
Could we abstract the services provided by that library behind some interfaces and swap the implementation of the same using PDFBox? 
