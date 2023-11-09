# llama.cpp

### Run StarCoder

```bash
# compile
make -j

# obtain the StarCoder model weights and place them in ./models
git clone https://huggingface.co/bigcode/starcoder
mv starcoder ./models
ls ./models/starcoder

# install Python environment and dependencies
conda create -n llama_cpp python=3.10
conda activate llama_cpp
pip install -r requirements.txt

# convert the 7B model to ggml FP16 format
python convert-starcoder-hf-to-gguf.py models/starcoder/ 1

# quantize the model to 4-bits (using q4_0 method)
./quantize ./models/starcoder/ggml-model-f16.gguf ./models/starcoder/ggml-model-q4_0.gguf q4_0


# run the inference
./main -m ./models/starcoder/ggml-model-q4_0.gguf -p "# Dijkstra's shortest path algorithm in Python (4 spaces indentation) + complexity analysis:\n\n" -e -t 4 --temp -1 -n 128
```
