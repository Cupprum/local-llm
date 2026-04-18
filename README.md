# Local LLM setup on Asahi Fedora 43 Macbook Pro M2 Pro 16 GB

This document describes how to setup `llama.cpp` to host LLMs, which are afterwards used in `opencode`.

## `llama.cpp` setup

How to install, build and run llama.cpp

**Install dependencies:**
```
sudo dnf update
sudo dnf install openssl-devel  vulkan-loader-devel vulkan-headers spirv-headers-devel glslc cmake clang git vulkan-tools
```

**Make scripts accessible:**

Link these files to `~/bin` folder:
```
cd ~/bin
ln -s ~/PP/local-llm/llm-server llm-server
ln -s ~/PP/local-llm/llm-ui llm-ui
ln -s ~/PP/local-llm/llm-cli llm-cli
```

**Build:**
```
cd llama.cpp

# Clean old build
rm -rf build

# Use Clang
export CC=clang
export CXX=clang++

# Use Vulkan and Openssl
cmake -B build -DGGML_VULKAN=1 -DLLAMA_OPENSSL=ON
cmake --build build --config Release
```

**Run:**
```
llm-server # Run llama-server on port 8033
llm-cli # Run llama-cli
llm-ui # Expose llama.cpp web ui
```
Configure model in `.env` file as `LOCAL_LLM_MODEL=ggml-org/gemma-4-E4B-it-GGUF:Q4_K_M`.
