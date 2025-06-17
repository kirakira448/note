# 基本流程
对于一个***ai自动化产品推广文案编写***工作流，基本流程如下：
1. 产品推广参数填写
2. agent生成文案
3. 确认文案内容
4. 自动发布

# 具体流程

## 1.配置agent-skill

搜索功能，生成图片功能，发布功能...

## 2.配置ai模型

  配置online-llm模型或local-llm模型
  用于下一步创建agent

## 3.配置agent

   a. 查找者 用于在本地知识库和网络搜索汇总资料
   b. 编辑者 使用汇总资料编写文案
   c. 发布者 使用编辑好的文案发布在社交平台上

## 4.定义work-flow

  需要尽可能详细，指出每一步使用哪一个agent执行哪个skill，结果交给谁
  例如：
         1.{查找者}使用{搜索}功能查找有关abc产品的评价，将结果以json的格式汇总，发送给{编辑者}
          2....


# 价格

## 总览
以openai为例，官网定价如下：

| Model                            | Input Cost per 1M Tokens     | Output Cost per 1M Tokens  |
| -------------------------------- | ---------------------------- | -------------------------- |
| gpt-4o                           | $5.00                        | $15.00                     |
| gpt-4-turbo                      | $10.00                       | $30.00                     |
| gpt-4                            | $30.00                       | $60.00                     |
| gpt-4-32k                        | $60.00                       | $120.00                    |
| gpt-3.5-turbo-0125               | $0.50                        | $1.50                      |
| gpt-3.5-turbo-instruct           | $1.50                        | $2.00                      |
| Fine-tuned gpt-3.5-turbo         | $8.00 (Training)             | $3.00                      |
| Fine-tuned davinci-002           | $6.00 (Training)             | $12.00                     |
| Fine-tuned babbage-002           | $0.40 (Training)             | $1.60                      |
| Embedding text-embedding-3-small | $0.02                        |                            |
| Embedding text-embedding-3-large | $0.13                        |                            |
| Embedding ada v2                 | $0.10                        |                            |
| Base davinci-002                 | $2.00                        |                            |
| Base babbage-002                 | $0.40                        |                            |
| Whisper (audio)                  | $0.006 per minute            |                            |
| TTS (audio)                      | $15.00 per 1M characters     |                            |
| TTS HD (audio)                   | $30.00 per 1M characters     |                            |
| DALL·E 3                         | $0.040 per image (standard)  | $0.080 per image (HD)      |
| DALL·E 2                         | $0.020 per image (1024x1024) | $0.018 per image (512x512) |

## 具体分析

### 基本单位
1k-token大约对应750个英文单词
对于一次完整的工作流程，大约需要如下token
$$
1k*t_{input}+3k*t_{output}
$$
以gpt-4o的定价为例

**计算**:

$$ 
 \text{Input Cost} = \left( \frac{1000 \text{ tokens}}{1,000,000 \text{ tokens}} \right) \times 5.00 \text{ dollars} = 0.005 \text{ dollars} 
$$
$$
\text{Output Cost} = \left( \frac{3000 \text{ tokens}}{1,000,000 \text{ tokens}} \right) \times 15.00 \text{ dollars} = 0.045 \text{ dollars}
$$

**总和**:

$$
\text{Unit Cost} = 0.005 \text{ dollars} + 0.045 \text{ dollars} = 0.05 \text{ dollars}
$$

即执行**一次工作流程**，大约花费**0.05美元**

### 月度开销

按照当前状况，假设每月主要有**3人**使用，每人月只推广**3个产品**，每次生成**20个文案**用于挑选
$$
\text{Month Cost} = \text{Unit Cost} \times3\times3\times5 \\
=0.05 \text{ dollars} \times 3 \times 3 \times 20=9\text{ dollars}
$$

即**一个月**的推广工作，大约花费**9美元**
**日元**：


## 本地跑llama3:70B

如果使用本地llm，可以省去api开销，但是可能对**硬件设备**有要求

想要在本地运行`llama3:70B`，推荐配置为：
- 显卡：24GB显存
- 内存：64GB

### 具体配置如下：

#### 总价:

- **处理器 (CPU)**: ¥4,000
- **显卡 (GPU)**: ¥15,000
- **主板 (Motherboard)**: ¥3,000
- **内存 (RAM)**: ¥3,500
- **存储 (Storage)**: ¥2,500
- **电源 (PSU)**: ¥900
- **机箱 (Case)**: ¥600
- **散热 (Cooling)**: ¥700
- **其他配件**: ¥100

**总计**: ¥ 30,300
**美元**: $ 4206
**日元**: ￥657963

#### 1. **处理器 (CPU)**

- **Intel Core i9-13900K** - 适用于高性能计算和AI任务
    - **价格**: ¥4,000

#### 2. **显卡 (GPU)**

- **NVIDIA Tesla P40** - 具有24GB显存，适用于深度学习和AI模型
    - **价格**: ¥15,000

#### 3. **主板 (Motherboard)**

- **ASUS ROG Strix Z690-E Gaming WiFi 6E** - 支持最新一代CPU和高性能RAM
    - **价格**: ¥3,000

#### 4. **内存 (RAM)**

- **Corsair Vengeance LPX 64GB (4 x 16GB) DDR5 5200MHz** - 高速运行内存
    - **价格**: ¥3,500

#### 5. **存储 (Storage)**

- **Samsung 970 EVO Plus 2TB NVMe M.2 SSD** - 高速存储和读取
    - **价格**: ¥2,500

#### 6. **电源 (PSU)**

- **Corsair RM850x 850W 80+ Gold** - 高效稳定的电源供应
    - **价格**: ¥900

#### 7. **机箱 (Case)**

- **NZXT H510 Flow** - 良好的散热和空间管理
    - **价格**: ¥600

#### 8. **散热 (Cooling)**

- **Noctua NH-D15** - 高效风冷系统，保证CPU的散热
    - **价格**: ¥700

#### 9. **其他配件**

- **Thermal Grizzly Kryonaut Thermal Paste** - 优质导热硅脂
    - **价格**: ¥100

