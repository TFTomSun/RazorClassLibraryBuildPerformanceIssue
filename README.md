# RazorClassLibraryBuildPerformanceIssue

Project Infos:
* RazorClassLibraryWithManyAssets has about 1400 small asset files
* Dependencies:
    * BlazorApp1 -> RazorClassLibraryConsumer -> RazorClassLibrary1 -> RazorClassLibraryWithManyAssets

Scenario 1:
* Make a little change in the ExampleJsInterop.cs of the RazorClassLibraryWithManyAssets project.
* build BlazorApp1
* Issue: every project in the build chain consumes more than 2 seconds to process the web assets from the project RazorClassLibraryWithManyAssets, which sums up in a 10sec build time.


Scenario 2:
* Make a little change in the ExampleJsInterop.cs of the RazorClassLibrary1 project.
* build RazorClassLibraryConsumer
* Issue: the project with many assets is up to date, wasn't build, but the assets still affect the build time of the other project significantly
