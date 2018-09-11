
# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.


# Building code
```
powershell .\build_all.ps1 -build
```

# Generating nupkg
From Visual Studio command prompt which has msbuild defined
```
powershell .\build_all.ps1 -build -generateNupkg
```

# Running Rest Server
```
pushd src\Microsoft.ServiceFabric.ReliableCollectionBackup\RestServer\
dotnet build
xcopy.exe /EIYS ..\..\..\packages\microsoft.servicefabric.tools.reliabilitysimulator\6.4.187-beta\lib\netstandard2.0\*.dll bin\Debug\net471\
dotnet run --no-build configs\sampleconfig.json

# test rest apis
curl -v http://localhost:5000/$query/testDictionary?$top=2

popd
```

# Running tests
```
pushd src\Microsoft.ServiceFabric.ReliableCollectionBackup\Parser.Tests
dotnet build
dotnet test --no-build --diag test_results.log --verbosity n --logger "console;verbosity=detailed"
popd

# running one test
dotnet test --no-build --diag test_results.log --verbosity n --logger "console;verbosity=detailed" --filter "FullyQualifiedName~BackupParser_EachTransactionHasRightChangesEvenWithBlockingTransactionAppliedEvents"
```

Running RestServer tests:
```
cd service-fabric-backup-explorer\src\Microsoft.ServiceFabric.ReliableCollectionBackup\RestServer.Tests
dotnet build && \
xcopy.exe /EIYS ..\..\..\packages\microsoft.servicefabric.tools.reliabilitysimulator\6.4.187-beta\lib\netstandard2.0\*.dll bin\Debug\net471\ && \
dotnet test --no-build --diag test_results.log --verbosity normal --logger "console;verbosity=detailed"
```
