# RazorClassLibraryBuildPerformanceIssue

Project Infos:
* RazorClassLibraryWithManyAssets has about 1400 small asset files
* Dependencies:
    * BlazorApp1 -> IndirectConsumerClassLibrary -> DirectConsumerClassLibrary -> RazorClassLibraryWithManyAssets

Scenario 1:
* Make a little change in the ExampleJsInterop.cs of the RazorClassLibraryWithManyAssets project.
* build BlazorApp1
* Issue: every project in the build chain consumes more than 2 seconds to process the web assets from the project RazorClassLibraryWithManyAssets, which sums up in a 10sec build time.


Scenario 2:
* Make a little change in the ExampleJsInterop.cs of the DirectConsumerClassLibrary project.
* build IndirectConsumerClassLibrary
* Issue: the project with many assets is up to date and wasn't build, the final app is also not built, but the assets still affect the build time of the library projects significantly


Scenario 3:
* Increase the number of web assets by copying the root folder several times and/or increase the build hierarchy depth by introducing new razor class libraries
* Do Scenario 1 and 2
* Issue: The build times explode!
