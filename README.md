# FreeIPA.DotNet

FreeIPA.DotNet is a client library for interacting with the FreeIPA API on the .NET platform. This library simplifies the HTTP requests required to communicate with a FreeIPA server.

## Usage

Below are examples of basic usage for the FreeIPA.DotNet library.

### Creating a Client

```csharp
using FreeIPA.DotNet;

var ipaClient = new IpaClient("https://ipa-server.example.com");
```

When creating a client, provide the base URL of your FreeIPA server.

### Logging in with Password

```csharp
using FreeIPA.DotNet.Dtos.Login;

var loginResult = await ipaClient.LoginWithPassword(new IpaLoginRequestDto
{
    Username = "admin",
    Password = "password123"
});

if (loginResult.Success)
{
    // Login successful
}
else
{
    // Login failed, check the error message
    var errorMessage = loginResult.Data.Message;
    Console.WriteLine($"Login failed: {errorMessage}");
}
```

To log in with a password, use the `LoginWithPassword` method. If the login is successful, the `Success` property will be true, and the response details will be available in the `Data` property. If the login fails, you can retrieve the error message from `Data.Message`.

### Sending an RPC Request

```csharp
using FreeIPA.DotNet.Dtos.RPC;

var rpcRequest = new IpaRpcRequestDto
{
    Method = "env",
    Parameters = new object[] { Array.Empty<string>(), new { } },
    Id = 0
};

var rpcResult = await ipaClient.SendRpcRequest(rpcRequest);

if (rpcResult.Success)
{
    // RPC request successful, use the results
    var response = rpcResult.Data;
    Console.WriteLine($"RPC response: {response}");
}
else
{
    // RPC request failed, check the error message
    var errorMessage = rpcResult.Data.Message;
    Console.WriteLine($"RPC request failed: {errorMessage}");
}
```

To send an RPC request, use the `SendRpcRequest` method. If the request is successful, the `Success` property will be true, and the response details will be available in the `Data` property. If the request fails, you can retrieve the error message from `Data.Message`.

## License
This project is licensed under the MIT License. For more information, see the [LICENSE](LICENSE) file.

## Issues, Feature Requests or Support
Please use the [New Issue](https://github.com/cynegeirus/dotnet-freeipa/issues/new) button to submit issues, feature requests or support issues directly to me. You can also send an e-mail to akin.bicer@outlook.com.tr.
