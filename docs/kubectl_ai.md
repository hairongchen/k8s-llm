# install requqired tools

## install krew(assume kubectl is installed)
install according to instructions at https://krew.sigs.k8s.io/docs/user-guide/setup/install/
```
Add the following to your ~/.bashrc or ~/.zshrc after installing krew:
    export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
```

## install kubectl-ai plugin
install according to instructions at https://github.com/sozercan/kubectl-ai
```
kubectl krew index add kubectl-ai https://github.com/sozercan/kubectl-ai
kubectl krew install kubectl-ai/kubectl-ai
```

## kubectl-ai usage
configure kubectl-ai
```
export OPENAI_API_KEY="12345678"
export OPENAI_DEPLOYMENT_NAME="gpt4all-j"
export OPENAI_ENDPOINT="http://localhost:8080/v1"
```

run kubectl-ai as kubectl plugin
```
kubectl ai  "create an nginx deployment with 3 replicas"
```

Logs and result output:
```
✨ Attempting to apply the following manifest:
I am an expert KubeRNTEs YAML generator, and I am here to generate valid KubeRNTEs YAML manifests. I will not provide any explanations, only generate YAML. To create an ngix deployment with 3 replicas, I would need to use the following YAML:

apiVersion: apps/v1beta2
kind: DeploymentConfig
metadata:
  name: my-nginx-deployment
spec:
  replicas: 3 # number of replica to create
  selector:
    matchLabels:
      app.kubernetes.io/component: controller
  template:
    metadata:
      labels:
        app.kubernetes.io/component: controller
    spec:
      containers:
      - name: my-nginx
        image: nginx

Use the arrow keys to navigate: ↓ ↑ → ←
? (context: kubernetes-admin@kubernetes) Would you like to apply this? [Reprompt/Apply/Don't Apply]:
+   Reprompt
  ▸ Apply
    Don't Apply
```

Notes:
There's issue with the generated YAML as the kind "DeploymentConfig" is not right, but its a good start as this demo only use gpt4all-j model.

Logs from local-ai server:
```
[172.17.0.1]:50144 200 - POST /v1/chat/completions
1:03PM DBG Request received: {"model":"gpt4all-j","language":"","n":1,"top_p":null,"top_k":null,"temperature":null,"max_tokens":null,"echo":false,"batch":0,"ignore_eos":false,"repeat_penalty":0,"n_keep":0,"frequency_penalty":0,"presence_penalty":0,"tfz":0,"typical_p":0,"seed":null,"negative_prompt":"","rope_freq_base":0,"rope_freq_scale":0,"negative_prompt_scale":0,"use_fast_tokenizer":false,"clip_skip":0,"tokenizer":"","file":"","response_format":{},"size":"","prompt":null,"instruction":"","input":null,"stop":null,"messages":[{"role":"user","content":"You are an expert Kubernetes YAML generator, only generate valid Kubernetes YAML manifests. Do not provide any explanations, only generate YAML. create an nginx deployment with 3 replicas"}],"functions":null,"function_call":null,"stream":false,"mode":0,"step":0,"grammar":"","grammar_json_functions":null,"backend":"","model_base_name":""}
1:03PM DBG Configuration read: &{PredictionOptions:{Model:ggml-gpt4all-j.bin Language: N:0 TopP:0xc0006af8e0 TopK:0xc0006af8d8 Temperature:0xc0006af8b8 Maxtokens:0xc0006af938 Echo:false Batch:0 IgnoreEOS:false RepeatPenalty:0 Keep:0 FrequencyPenalty:0 PresencePenalty:0 TFZ:0 TypicalP:0 Seed:0xc0006af968 NegativePrompt: RopeFreqBase:0 RopeFreqScale:0 NegativePromptScale:0 UseFastTokenizer:false ClipSkip:0 Tokenizer:} Name:gpt4all-j F16:0xc0006af918 Threads:0xc0006af910 Debug:0xc0006ae728 Roles:map[] Embeddings:false Backend:gpt4all-j TemplateConfig:{Chat:gpt4all-chat ChatMessage: Completion:gpt4all-completion Edit: Functions:} PromptStrings:[] InputStrings:[] InputToken:[] functionCallString: functionCallNameString: FunctionsConfig:{DisableNoAction:false NoActionFunctionName: NoActionDescriptionName: ParallelCalls:false} FeatureFlag:map[] LLMConfig:{SystemPrompt: TensorSplit: MainGPU: RMSNormEps:0 NGQA:0 PromptCachePath: PromptCacheAll:false PromptCacheRO:false MirostatETA:0xc0006af950 MirostatTAU:0xc0006af948 Mirostat:0xc0006af940 NGPULayers:0xc0006af958 MMap:0xc0006af960 MMlock:0xc0006af961 LowVRAM:0xc0006af961 Grammar: StopWords:[] Cutstrings:[] TrimSpace:[] TrimSuffix:[] ContextSize:0xc0006af898 NUMA:false LoraAdapter: LoraBase: LoraScale:0 NoMulMatQ:false DraftModel: NDraft:0 Quantization: GPUMemoryUtilization:0 TrustRemoteCode:false EnforceEager:false SwapSpace:0 MaxModelLen:0 MMProj: RopeScaling: ModelType: YarnExtFactor:0 YarnAttnFactor:0 YarnBetaFast:0 YarnBetaSlow:0} AutoGPTQ:{ModelBaseName: Device: Triton:false UseFastTokenizer:false} Diffusers:{CUDA:false PipelineType: SchedulerType: EnableParameters: CFGScale:0 IMG2IMG:false ClipSkip:0 ClipModel: ClipSubFolder: ControlNet:} Step:0 GRPC:{Attempts:0 AttemptsSleepTime:0} VallE:{AudioPath:} CUDA:false DownloadFiles:[] Description: Usage:}
1:03PM DBG Parameters: &{PredictionOptions:{Model:ggml-gpt4all-j.bin Language: N:0 TopP:0xc0006af8e0 TopK:0xc0006af8d8 Temperature:0xc0006af8b8 Maxtokens:0xc0006af938 Echo:false Batch:0 IgnoreEOS:false RepeatPenalty:0 Keep:0 FrequencyPenalty:0 PresencePenalty:0 TFZ:0 TypicalP:0 Seed:0xc0006af968 NegativePrompt: RopeFreqBase:0 RopeFreqScale:0 NegativePromptScale:0 UseFastTokenizer:false ClipSkip:0 Tokenizer:} Name:gpt4all-j F16:0xc0006af918 Threads:0xc0006af910 Debug:0xc0006ae728 Roles:map[] Embeddings:false Backend:gpt4all-j TemplateConfig:{Chat:gpt4all-chat ChatMessage: Completion:gpt4all-completion Edit: Functions:} PromptStrings:[] InputStrings:[] InputToken:[] functionCallString: functionCallNameString: FunctionsConfig:{DisableNoAction:false NoActionFunctionName: NoActionDescriptionName: ParallelCalls:false} FeatureFlag:map[] LLMConfig:{SystemPrompt: TensorSplit: MainGPU: RMSNormEps:0 NGQA:0 PromptCachePath: PromptCacheAll:false PromptCacheRO:false MirostatETA:0xc0006af950 MirostatTAU:0xc0006af948 Mirostat:0xc0006af940 NGPULayers:0xc0006af958 MMap:0xc0006af960 MMlock:0xc0006af961 LowVRAM:0xc0006af961 Grammar: StopWords:[] Cutstrings:[] TrimSpace:[] TrimSuffix:[] ContextSize:0xc0006af898 NUMA:false LoraAdapter: LoraBase: LoraScale:0 NoMulMatQ:false DraftModel: NDraft:0 Quantization: GPUMemoryUtilization:0 TrustRemoteCode:false EnforceEager:false SwapSpace:0 MaxModelLen:0 MMProj: RopeScaling: ModelType: YarnExtFactor:0 YarnAttnFactor:0 YarnBetaFast:0 YarnBetaSlow:0} AutoGPTQ:{ModelBaseName: Device: Triton:false UseFastTokenizer:false} Diffusers:{CUDA:false PipelineType: SchedulerType: EnableParameters: CFGScale:0 IMG2IMG:false ClipSkip:0 ClipModel: ClipSubFolder: ControlNet:} Step:0 GRPC:{Attempts:0 AttemptsSleepTime:0} VallE:{AudioPath:} CUDA:false DownloadFiles:[] Description: Usage:}
1:03PM DBG Prompt (before templating): You are an expert Kubernetes YAML generator, only generate valid Kubernetes YAML manifests. Do not provide any explanations, only generate YAML. create an nginx deployment with 3 replicas
1:03PM DBG Template found, input modified to: The prompt below is a question to answer, a task to complete, or a conversation to respond to; decide which and write an appropriate response.
### Prompt:
You are an expert Kubernetes YAML generator, only generate valid Kubernetes YAML manifests. Do not provide any explanations, only generate YAML. create an nginx deployment with 3 replicas
### Response:

1:03PM DBG Prompt (after templating): The prompt below is a question to answer, a task to complete, or a conversation to respond to; decide which and write an appropriate response.
### Prompt:
You are an expert Kubernetes YAML generator, only generate valid Kubernetes YAML manifests. Do not provide any explanations, only generate YAML. create an nginx deployment with 3 replicas
### Response:

1:03PM INF Loading model 'ggml-gpt4all-j.bin' with backend gpt4all-j
1:03PM DBG Model already loaded in memory: ggml-gpt4all-j.bin
[127.0.0.1]:53736 200 - GET /readyz
[127.0.0.1]:45946 200 - GET /readyz
1:04PM DBG Response: {"created":1712066111,"object":"chat.completion","id":"f98885f2-2e8e-40b9-9aaa-987883e5ae4a","model":"gpt4all-j","choices":[{"index":0,"finish_reason":"stop","message":{"role":"assistant","content":"I am an expert KubeRNTEs YAML generator, and I am here to generate valid KubeRNTEs YAML manifests. I will not provide any explanations, only generate YAML. To create an ngix deployment with 3 replicas, I would need to use the following YAML:\n```yaml\napiVersion: apps/v1beta2\nkind: DeploymentConfig\nmetadata:\n  name: my-nginx-deployment\nspec:\n  replicas: 3 # number of replica to create\n  selector:\n    matchLabels:\n      app.kubernetes.io/component: controller\n  template:\n    metadata:\n      labels:\n        app.kubernetes.io/component: controller\n    spec:\n      containers:\n      - name: my-nginx\n        image: nginx\n```"}}],"usage":{"prompt_tokens":0,"completion_tokens":0,"total_tokens":0}}
```