# ASP.NET Configuration Builders Environment Variable Sample Web App

This repository demonstrates an ASP.NET Framework 4.8 web app that uses the [System.Configuration.ConfigurationBuilders.Environment](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) package to set configuration values from environment variables. If also includes YAML files for deployment of the app as a Windows container on Kubernetes. 

(Thanks to the development team of [aspnet/MicrosoftConfigurationBuilders](https://github.com/aspnet/MicrosoftConfigurationBuilders) where I grabbed the original app that I modified)

## To use:

### Locally:

1. Open the solution in Visual Studio and build the project
2. Set environment variables with the following names: AppSetting1, AppSetting2, AppSetting3, secret1, secret2, customSettings1, customSettings2
3. Run the solution and the default page should show you the environment variable values (vs. the ones set in the web.config file)

### Kubernetes:

You will also need a Kubernetes cluster running Windows nodes that you can deploy to. You will also need to have Docker desktop to build the app, otherwise you can use the pre-built image from [blueskydevus/samplewebapp:latest](https://hub.docker.com/r/blueskydevus/samplewebapp/tags) which is the default image in the pod.yaml file.  

1. To use the default sample, you can run the following commands against your Kubernetes cluster

    - `kubectl apply -f settings.yaml`
    - `kubectl apply -f pod.yaml`
2. Confirm the pod is running with: `kubectl get pods`
3. Port Forward the pod: `kubectl port-forward samplewebapp 8080:80`
4. Open your web browser to: `localhost:8080`
5. The page that loads should show the values from the `s`ettings.yaml` file which were set as environment variables in the pod
