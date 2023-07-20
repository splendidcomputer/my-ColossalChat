# my-ColossalChat

Please, following the forth comming commands in order to setup the ColossalChat project on your Debian-based Machine:

First, you need to ensure that you have the `venv` module installed. In Python 3.3 and later, it is included by default. If you need to install it separately, you can do so by running:
   
   ```
   sudo apt-get install python3-venv
   ```
   
## Install

```
conda create -n coati
conda activate coati
conda install cudatoolkit=11.7 -c nvidia
git clone https://github.com/hpcaitech/ColossalAI.git
cd ColossalAI
python3 -m venv venv
source venv/bin/activate
cd applications/Chat
pip install .
```

## Install the Transformers

```
rm -r transformers/
git clone https://github.com/hpcaitech/transformers
cd transformers/
pip install .
cd ../examples
pip install -r requirements.txt
```

## Download Datasets
```
git clone https://github.com/XueFuzhao/InstructionWild.git
cd data
curl -L -o instinwild_en.json 'https://drive.google.com/uc?export=download&id=1qOfrl0RIWgH2_b1rYCEVxjHF3u3Dwqay'
curl -L -o instinwild_ch.json 'https://drive.google.com/uc?export=download&id=1OqfOUWYfrK6riE9erOx-Izp3nItfqz_K'

```

## Stage I: Supervised Learning:

```
cd ../..
scp train_sft.sh train_sft.sh.bak
sudo apt-get install git-lfs
git clone https://huggingface.co/bigscience/bloom-560m

```

### Modify the train_sft.sh file:

```
echo 'torchrun --standalone --nproc_per_node=1 train_sft.py \\' > train_sft.sh
echo '    --pretrain "bloom-560m" \\' >> train_sft.sh
echo "    --model 'bloom' \\" >> train_sft.sh
echo '    --strategy colossalai_zero2 \\' >> train_sft.sh
echo '    --log_interval 10 \\' >> train_sft.sh
echo '    --save_path  output \\' >> train_sft.sh
echo '    --dataset InstructionWild/data/instinwild_en.json \\' >> train_sft.sh
echo '    --batch_size 4 \\' >> train_sft.sh
echo '    --accumulation_steps 8 \\' >> train_sft.sh
echo '    --lr 2e-5 \\' >> train_sft.sh
echo '    --max_datasets_size 512 \\' >> train_sft.sh
echo '    --max_epochs 1' >> train_sft.sh
```
### Enaable the training
```
chmod +x ./train_sft.sh
./train_sft.sh
```
