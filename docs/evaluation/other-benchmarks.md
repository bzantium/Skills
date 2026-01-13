# Other benchmarks

More details are coming soon!

## Supported benchmarks

### arena-hard

- Benchmark is defined in [`nemo_skills/dataset/arena-hard/__init__.py`](https://github.com/NVIDIA-NeMo/Skills/blob/main/nemo_skills/dataset/arena-hard/__init__.py)
- Original benchmark source is [here](https://github.com/lmarena/arena-hard-auto).
- Uses `gpt-4.1` as the default judge model for evaluation.
- Uses `gpt-4-0314` model's responses as reference answers (baseline answers) for comparison.

#### Data Preparation

First, prepare the dataset by running the `ns prepare_data` command.

```bash
ns prepare_data arena-hard
```

#### Running the Evaluation

Once the data is prepared, you can run the evaluation. Replace `<...>` placeholders with your cluster and directory paths.

```bash
ns eval \
    --cluster=<CLUSTER_NAME> \
    --model=nvidia/NVIDIA-Nemotron-3-Nano-30B-A3B-FP8 \
    --server_type=vllm \
    --server_gpus=8 \
    --benchmarks=arena-hard \
    --data_dir=/workspace/ns-data/arena-hard \
    --output_dir=<OUTPUT_DIR> \
    ++parse_reasoning=True \
    ++inference.temperature=0.6 \
    ++inference.top_p=0.95 \
    ++inference.tokens_to_generate=32768
```

#### Verifying Results

After all jobs are complete, you can check the results in `<OUTPUT_DIR>/eval-results/arena-hard/metrics.json`.

```
------------------------------------------- arena-hard -------------------------------------------
evaluation_mode | num_entries | score  | 95_CI         | invalid_scores | avg_tokens | gen_seconds
pass@1          | 500         | 94.82% | (-0.67, 0.69) | 0              | 3878       | 230
```

### arena-hard-v2

- Benchmark is defined in [`nemo_skills/dataset/arena-hard-v2/__init__.py`](https://github.com/NVIDIA-NeMo/Skills/blob/main/nemo_skills/dataset/arena-hard-v2/__init__.py)
- Original benchmark source is [here](https://github.com/lmarena/arena-hard-auto).
- Uses `o3-mini-2025-01-31` as the default judge model for evaluation.
- Uses `o3-mini-2025-01-31` model's responses as reference answers (baseline answers) for comparison.

#### Data Preparation

First, prepare the dataset by running the `ns prepare_data` command.

```bash
ns prepare_data arena-hard-v2
```

#### Running the Evaluation

Once the data is prepared, you can run the evaluation. Replace `<...>` placeholders with your cluster and directory paths.

```bash
ns eval \
    --cluster=<CLUSTER_NAME> \
    --model=nvidia/NVIDIA-Nemotron-3-Nano-30B-A3B-FP8 \
    --server_type=vllm \
    --server_gpus=8 \
    --benchmarks=arena-hard-v2 \
    --data_dir=/workspace/ns-data/arena-hard-v2 \
    --output_dir=<OUTPUT_DIR> \
    ++parse_reasoning=True \
    ++inference.temperature=0.6 \
    ++inference.top_p=0.95 \
    ++inference.tokens_to_generate=32768
```

#### Verifying Results

After all jobs are complete, you can check the results in `<OUTPUT_DIR>/eval-results/arena-hard-v2/metrics.json`.

```
----------------------------------------- arena-hard-v2 ------------------------------------------
evaluation_mode | num_entries | score  | 95_CI         | invalid_scores | avg_tokens | gen_seconds
pass@1          | 750         | 64.15% | (-1.74, 1.55) | 0              | 4309       | 101
```