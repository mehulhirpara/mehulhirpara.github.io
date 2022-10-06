## Exploring Azure web app deployment option as a beginner

I have decided to deploy my web app on Azure for the first time and I found Azure provides multiple ways to deploy a web app, mobile app backend, or API app. I referred to https://learn.microsoft.com/en-us/azure/app-service/ and found the following different options:
1. Upload content with FTP
2. Deploy zip packages and individual files
3. Local Git deployment to Azure App Service
4. Sync content from a cloud folder to Azure App Service
5. Continuous deployment to Azure App Service
6. Run your app directly from a zip package

Apart from the above-mentioned methods, Visual Studio Code IDE also provides [Azure extensions](https://code.visualstudio.com/docs/azure/deployment) that can be used to deploy web apps right from the IDE itself with a few quick steps. Since I'm using Visual Studio Code as my preferred IDE, I decided to go with the Azure extensions.

<img align="center" width="20%" height="20%" src="https://user-images.githubusercontent.com/15310228/194284002-52e20620-e72a-4a34-a346-9b29fc04f6f7.png">

Created a basic web app instance on Azure:

<img align="center" width="20%" height="20%" src="https://user-images.githubusercontent.com/15310228/194286065-c7eb1158-18a4-4f2f-875a-d1aa5f5f5efb.png">

Synced web app service instance to Visual Studio Code:

<img align="center" width="20%" height="20%" src="https://user-images.githubusercontent.com/15310228/194289032-84c00ceb-174c-4686-bff2-d81f6d92b7d5.png">

Deployed sample Node.JS app with just right-clicking on app instance:

<img align="center" width="20%" height="20%" src="https://user-images.githubusercontent.com/15310228/194290273-1f726cfa-7a2c-4731-b88b-e23ceb9983e4.png">

The code has been zipped and uploaded automatically by the extension. After some time, I found the following error:

<img align="center" width="50%" height="50%" src="https://user-images.githubusercontent.com/15310228/194289798-cec6535a-3b06-4591-bcee-d1686197a338.png">

After checking logs and with multiple trails, I found that the app service instance (container) is crashing due to higher RAM requirements during the `npm run build`. Then I created another instance with Basic Service Plan, which provides 1.75 GB RAM, and the issue is resolved.

<img align="center" width="50%" height="50%" src="https://user-images.githubusercontent.com/15310228/194291552-a22e348c-a3dd-40c7-a2a2-290e3d860e7b.png">

In conclusion, I could be able to deploy the web app using the Azure extension of VS Code but ran into errors and ended up paying extra for the requirement of higher RAM only to rebuild the web app.

Reserving extra RAM could be a costly option as re-building is required only to apply new changes. Can there be a better option or method?

Digging more, I found a better option which is [deploy-run-package](https://learn.microsoft.com/en-us/azure/app-service/deploy-run-package). Here, the idea is to verify the app locally first by building it, zipping it, and then pushing it to the app service instance. This method has multiple advantages, as described in its documentation, plus I would like to highlight one more advantage, that deployment is now cost-effective and no more extra RAM is required.

While following [deploy-run-package](https://learn.microsoft.com/en-us/azure/app-service/deploy-run-package), make sure disk space is available to push the zip file as errors are yet to be more descriptive.
