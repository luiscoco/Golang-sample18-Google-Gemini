# Golang: Google Cloud Gemini Vertex AI API call to describe an image

This is the official Google sample web page: https://cloud.google.com/vertex-ai/docs/generative-ai/start/quickstarts/quickstart-multimodal

## 1. Run VSCode and copy this code

```


```

```

```

## 2. Create the "go.mod" file

## 3. Create the "go.sum" file

If a specific package is causing issues, you can try fetching it directly using go get. For example:

```
go get github.com/googleapis/enterprise-certificate-proxy@v0.3.2
```

## 4. Run the application



## 5. Verify the image content

We open the Donwload folder and we download the image with this command

```
gsutil cp gs://generativeai-downloads/images/scones.jpg ./scones.jpg
```

![image](https://github.com/luiscoco/Golang-sample18-Google-Gemini/assets/32194879/256876ad-f92f-4ead-afd8-052e3f6465f6)

We see the image 

![image](https://github.com/luiscoco/Golang-sample18-Google-Gemini/assets/32194879/e8848059-b7b1-46f7-a594-7a4312fd9aaa)

![image](https://github.com/luiscoco/Golang-sample18-Google-Gemini/assets/32194879/8b2d03f4-7aa0-49e0-bb24-d60419ffbf39)

This is the description we got from Gemini:

**There are six blueberry scones on a white napkin with blueberries scattered around. There is a silver spoon on one scone that says Let's Jam. There are also three pink peonies and two cups of coffee.**

![image](https://github.com/luiscoco/Golang-sample18-Google-Gemini/assets/32194879/a18fa656-14c1-445f-a734-e8e85d324e5d)




