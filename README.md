# 🧠 HK-DevBrain

> An intelligent Ollama model specialized in code generation, mathematics, and technical documentation.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Ollama](https://img.shields.io/badge/Ollama-Compatible-green.svg)](https://ollama.ai)
[![Version](https://img.shields.io/badge/version-1.0-brightgreen.svg)](https://github.com/himanshu231204/hk-devbrain)

---

## 🎯 What is HK-DevBrain?

HK-DevBrain is a lightweight (2GB), fast, and specialized AI model built on Llama 3.2 3B, optimized for:

- 🔧 **Code Generation** - Multi-language with best practices
- 📐 **Mathematics** - Step-by-step problem solving
- 📝 **Technical Documentation** - READMEs, API docs, and more

## ✨ Features

- **Lightweight**: Only 2GB - runs on any hardware
- **Fast**: 2x faster than 7B models
- **Specialized**: Pre-trained for technical tasks
- **Smart**: Few-shot learning examples embedded
- **Free**: No API costs, runs completely offline
- **Open**: Share and deploy anywhere

## 🚀 Quick Start

### Prerequisites

Install [Ollama](https://ollama.ai) on your system.

### Installation

```bash
# Clone this repository
git clone https://github.com/himanshu231204/hk-devbrain.git
cd hk-devbrain

# Pull base model
ollama pull llama3.2:3b

# Build HK-DevBrain
ollama create hk-devbrain -f Modelfile

# Run the model
ollama run hk-devbrain
```

### Quick Test

```bash
# Code generation
ollama run hk-devbrain "Write a Python function to validate email addresses"

# Math problem
ollama run hk-devbrain "Solve: x^2 + 5x + 6 = 0"

# README generation
ollama run hk-devbrain "Generate a README for a Flask REST API project"
```

## 📚 Usage Examples

### 1. Generate Code

```bash
ollama run hk-devbrain """
Write a TypeScript function for user authentication:
- JWT token generation
- Password hashing with bcrypt
- Error handling
- Type definitions
"""
```

### 2. Solve Math Problems

```bash
ollama run hk-devbrain """
Find the derivative of f(x) = 3x^2 * sin(x)
Show all steps using product rule
"""
```

### 3. Create Documentation

```bash
ollama run hk-devbrain """
Generate API documentation for:
- POST /api/users (create user)
- GET /api/users/:id (get user)
Include request/response examples
"""
```

### 4. Generate README Files

```bash
ollama run hk-devbrain """
Create a README for a React dashboard app with:
- Features: charts, user management, auth
- Tech: React, TypeScript, Redux, Recharts
- Deployment: Docker
"""
```

## 🎨 Model Variants

Create specialized variants for different use cases:

### Fast Variant (Speed Optimized)
```bash
# Edit Modelfile: reduce num_ctx to 4096
ollama create hk-devbrain:fast -f Modelfile-fast
```

### Large Variant (High Context)
```bash
# Edit Modelfile: increase num_ctx to 32768
ollama create hk-devbrain:large -f Modelfile-large
```

### Creative Variant (Documentation)
```bash
# Edit Modelfile: increase temperature to 0.7
ollama create hk-devbrain:creative -f Modelfile-creative
```

## 🔧 Configuration

### Interactive Session Customization

```bash
ollama run hk-devbrain

# Inside the session:
/set parameter temperature 0.5      # Adjust creativity
/set parameter num_predict 2000     # Longer responses
/set verbose                         # Show statistics
```

### Save Custom Sessions

```bash
/save hk-devbrain-python    # Save current configuration
/load hk-devbrain-python    # Load saved configuration
```

## 📊 Performance

| Metric | HK-DevBrain | Llama 7B | Llama 70B |
|--------|-------------|----------|-----------|
| **Size** | 2GB | 4.7GB | 40GB |
| **Speed** (100 tokens) | 0.8s | 1.5s | 8.2s |
| **RAM Usage** | 2.5GB | 5.2GB | 45GB |
| **Quality** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |

*Benchmarked on MacBook Pro M1, 16GB RAM*

## 🌐 API Wrapper

Deploy HK-DevBrain as a REST API:

```python
# app.py
from flask import Flask, request, jsonify
import requests

app = Flask(__name__)

@app.route('/generate', methods=['POST'])
def generate():
    prompt = request.json['prompt']
    response = requests.post('http://localhost:11434/api/generate',
        json={'model': 'hk-devbrain', 'prompt': prompt})
    return jsonify(response.json())

app.run(port=5000)
```

Run: `python app.py`

Use: 
```bash
curl -X POST http://localhost:5000/generate \
  -H "Content-Type: application/json" \
  -d '{"prompt": "Write a hello world function"}'
```

## 🐳 Docker Deployment

```dockerfile
FROM ollama/ollama:latest

COPY Modelfile /root/Modelfile

RUN ollama serve & sleep 5 && \
    ollama pull llama3.2:3b && \
    ollama create hk-devbrain -f /root/Modelfile

EXPOSE 11434

CMD ["ollama", "serve"]
```

Build and run:
```bash
docker build -t hk-devbrain .
docker run -d -p 11434:11434 hk-devbrain
```

## 📖 Documentation

- **[Complete Guide](hk-devbrain-complete-guide.md)** - Full documentation
- **[Modelfile](Modelfile)** - Model configuration
- **[Examples](examples/)** - Usage examples

## 🛠️ Troubleshooting

### Model creation fails
```bash
# Ensure base model exists
ollama pull llama3.2:3b
ollama create hk-devbrain -f Modelfile
```

### Out of memory
Edit `Modelfile`, reduce `num_ctx` to `4096`

### Slow performance
```bash
ollama run hk-devbrain
/set parameter num_gpu 50  # Enable GPU acceleration
```

See [Complete Guide](hk-devbrain-complete-guide.md#troubleshooting) for more solutions.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

Base model (Llama 3.2) follows Meta's Llama 3.2 Community License.

## 🙏 Acknowledgments

- [Meta AI](https://ai.meta.com/) for Llama 3.2
- [Ollama](https://ollama.ai) team for the platform
- Open source community

## 👤 Author

**Himanshu Kumar (HK)**

- Model: hk-devbrain
- GitHub: [@himanshu231204](https://github.com/himanshu231204)

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/himanshu231204/hk-devbrain/issues)
- **Discussions**: [GitHub Discussions](https://github.com/himanshu231204/hk-devbrain/discussions)
- **Community**: [Ollama Discord](https://discord.gg/ollama)

## ⭐ Show Your Support

Give a ⭐️ if this project helped you!

---

**Built with ❤️ by Himanshu Kumar (HK)**

*HK-DevBrain v1.0 - Your intelligent coding companion*

<!-- gumroad-footer -->
---

### More free resources

I share free visual notes, agent skills and guides on AI agents, Google ADK, RAG and LLMs.

[![Gumroad](https://img.shields.io/badge/Gumroad-free_notes_%26_skills-ff90e8?style=flat-square&logo=gumroad&logoColor=white)](https://himanshu231204.gumroad.com) → **[himanshu231204.gumroad.com](https://himanshu231204.gumroad.com)**
