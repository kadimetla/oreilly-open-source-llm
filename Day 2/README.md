# Day 2 for LLM Bootcamp

On day 2, we will concentrate on *decoder models*, also
called GPT-like models. These models can be used for
completing text, or answering questions (in the style
of ChatGPT). As this use case is much more popular,
we will focus on this.

## Presentation
The [slides](<2025-11-19-LLM-3-1.pdf>) contain additional
background and theroretical information.

## Notebooks

You can either try to run the notebooks directly
or try to follow how I run them and use it as a 
documentation (or run it later).
* [11-qwen3.5-9b.ipynb](11-qwen3.5-9b.ipynb: Run a Qwen3.5 model with the `transformers` library)
* [12-gemma4-e4b.ipynb](12-gemma4-e4b.ipynb: Run a Gemma 4 model with the `transformers` library)
* [21-vllm-direct.ipynb](21-vllm-direct.ipynb: Use `vllm` as a runtime environment instead of `transformers`)
* [22-vllm-direct-awq.ipynb](22-vllm-direct-awq.ipynb: Use `vllm` with quantization as a runtime environment instead of `transformers`)
* [23-vllm-api.ipynb](23-vllm-api.ipynb: Use `vllm` as a server)
* [24-tabbyAPI.ipynb](24-tabbyAPI.ipynb: Use `tabbyAPI` as a server)
* [25-llama-cpp.ipynb](25-llama-cpp.ipynb: Use `llama.cpp` as a server)



### Text generation using `transformers`

## Running LLMs on the CPU

For this, a good starting point is [LM Studio](https://lmstudio.ai/) which is available for all major platforms. However, it is not Open Source Software.

An alternative (but also not completely open) is [ollama](https://ollama.com/).

If you want to run free software, [llama.cpp](https://github.com/ggml-org/llama.cpp) is recommended. It is a very active project with multiple releases per day and supports many current models. `llama.cpp` can also run as server and is compatible to the OpenAI API.

### Creating your own GGUFs

The easiest way is to download GGUFs, which are widely available on [Hugging Face](https://huggingface.co).

If a GGUF is not available, you can also [create it there](https://huggingface.co/spaces/ggml-org/gguf-my-repo).

Using llama.cpp, you can convert Hugging Face repositories (download first via `huggingface-cli download --local-dir Qwen-8B Qwen/Qwen3-8B`) to GGUF:

```bash
python convert_hf_to_gguf.py --outfile Qwen3-8B.gguf Qwen3-8B
```

Afterwards, you can quantize them:

```bash
$ build/bin/llama-quantize Qwen3-8B.gguf Qwen3-8B-Q4_K_M.gguf q4_k_m
```

Finally, run a `llama-server` to access the frontend:

```bash
$ build/bin/llama-server -m Qwen3-8B-Q4_K_M.gguf --port 8080
```

## Trying models without local hardware

On [Hugging Face](https://huggingface.co), some models
are available for inference.

You can also try [OpenRouter](https://openrouter.ai/models),
some of the models are free, for some you have to pay (very
little). Many new models are available there.
