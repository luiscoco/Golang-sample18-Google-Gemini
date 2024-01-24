# Golang: Google Cloud Gemini Vertex AI API call to describe an image

This sample source code: https://github.com/luiscoco/Golang-sample18-Google-Gemini/

This is the official Google sample web page: 

https://cloud.google.com/vertex-ai/docs/generative-ai/start/quickstarts/quickstart-multimodal

## 1. Run VSCode and copy this code

![image](https://github.com/luiscoco/Golang-sample18-Google-Gemini/assets/32194879/970a0021-1704-4379-b786-dfe736bb2d80)

```go
// Copyright 2023 Google LLC
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
//     http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

// multimodal shows an example of understanding multimodal input
package main

import (
	"context"
	"fmt"
	"io"
	"log"
	"mime"
	"os"
	"path/filepath"

	"cloud.google.com/go/vertexai/genai"
)

func main() {
	projectID := os.Getenv("GOOGLE_CLOUD_PROJECT")
	location := "us-central1"
	modelName := "gemini-pro-vision"

	prompt := "describe what is in this picture"
	image := "gs://generativeai-downloads/images/scones.jpg"

	if projectID == "" {
		log.Fatal("require environment variable GOOGLE_CLOUD_PROJECT")
	}

	err := generateMultimodalContent(os.Stdout, prompt, image, projectID, location, modelName)
	if err != nil {
		log.Fatalf("unable to generate: %v", err)
	}
}

// generateMultimodalContent generates a response into w, based upon the prompt
// and image provided.
func generateMultimodalContent(w io.Writer, prompt, image, projectID, location, modelName string) error {
	ctx := context.Background()

	client, err := genai.NewClient(ctx, projectID, location)
	if err != nil {
		return fmt.Errorf("unable to create client: %v", err)
	}
	defer client.Close()

	model := client.GenerativeModel(modelName)
	model.SetTemperature(0.4)

	// Given an image file URL, prepare image file as genai.Part
	img := genai.FileData{
		MIMEType: mime.TypeByExtension(filepath.Ext(image)),
		FileURI:  image,
	}

	res, err := model.GenerateContent(ctx, img, genai.Text(prompt))
	if err != nil {
		return fmt.Errorf("unable to generate contents: %v", err)
	}

	fmt.Fprintf(w, "generated response: %s\n", res.Candidates[0].Content.Parts[0])
	return nil
}
```

## 2. We store the PROJECT_ID in an environmental variable

![image](https://github.com/luiscoco/Golang-sample18-Google-Gemini/assets/32194879/420e518e-4019-4e9e-8d13-10322aedef2e)

## 3. Create the "go.mod" file

We create the **go.mod**

```
module github.com/GoogleCloudPlatform/golang-samples/vertexai/multimodal

go 1.21.6

require (
	cloud.google.com/go/vertexai v0.6.0
)

require (
	cloud.google.com/go v0.111.0 // indirect
	cloud.google.com/go/aiplatform v1.58.0 // indirect
	cloud.google.com/go/compute v1.23.3 // indirect
	cloud.google.com/go/compute/metadata v0.2.3 // indirect
	cloud.google.com/go/iam v1.1.5 // indirect
	cloud.google.com/go/longrunning v0.5.4 // indirect
	cloud.google.com/go/storage v1.36.0 // indirect
	github.com/felixge/httpsnoop v1.0.4 // indirect
	github.com/go-logr/logr v1.3.0 // indirect
	github.com/go-logr/stdr v1.2.2 // indirect
	github.com/golang/groupcache v0.0.0-20210331224755-41bb18bfe9da // indirect
	github.com/golang/protobuf v1.5.3 // indirect
	github.com/google/s2a-go v0.1.7 // indirect
	github.com/google/uuid v1.5.0 // indirect
	github.com/googleapis/enterprise-certificate-proxy v0.3.2 // indirect
	github.com/googleapis/gax-go/v2 v2.12.0 // indirect
	go.opencensus.io v0.24.0 // indirect
	go.opentelemetry.io/contrib/instrumentation/google.golang.org/grpc/otelgrpc v0.46.1 // indirect
	go.opentelemetry.io/contrib/instrumentation/net/http/otelhttp v0.46.1 // indirect
	go.opentelemetry.io/otel v1.21.0 // indirect
	go.opentelemetry.io/otel/metric v1.21.0 // indirect
	go.opentelemetry.io/otel/trace v1.21.0 // indirect
	golang.org/x/crypto v0.18.0 // indirect
	golang.org/x/net v0.20.0 // indirect
	golang.org/x/oauth2 v0.16.0 // indirect
	golang.org/x/sync v0.6.0 // indirect
	golang.org/x/sys v0.16.0 // indirect
	golang.org/x/text v0.14.0 // indirect
	golang.org/x/time v0.5.0 // indirect
	google.golang.org/api v0.156.0 // indirect
	google.golang.org/appengine v1.6.8 // indirect
	google.golang.org/genproto v0.0.0-20240108191215-35c7eff3a6b1 // indirect
	google.golang.org/genproto/googleapis/api v0.0.0-20240102182953-50ed04b92917 // indirect
	google.golang.org/genproto/googleapis/rpc v0.0.0-20240102182953-50ed04b92917 // indirect
	google.golang.org/grpc v1.60.1 // indirect
	google.golang.org/protobuf v1.32.0 // indirect
)
```

## 4. Create the "go.sum" file

We run the this command to create the **go.sum**

```
go mod tidy
```

If a specific package is causing issues, you can try fetching it directly using go get. For example:

```
go get github.com/googleapis/enterprise-certificate-proxy@v0.3.2
```

## 5. Run the application

We execute the application with the command

```
go run multimodal.go
```

![image](https://github.com/luiscoco/Golang-sample18-Google-Gemini/assets/32194879/71d3528a-7e78-475d-a254-74772388f4f6)

## 6. Verify the image content

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




