# AuToTeX: From Handwriting to LaTeX in Seconds 

## The Problem We've All Faced 
*How many times have you been here?* You're sitting in a class or meeting, **frantically scribbling** information on paper. In the moment, it seems manageable, but later...
- Your handwriting looks like ancient hieroglyphics
- Papers are scattered everywhere
- You wish you had a clean, professional PDF
- Those complex math equations? Good luck typing those up!

## Why Hasn't This Been Solved? 
We've had OCR (Optical Character Recognition) tools for *many decades*. They're great for converting typed text, but what about:
- Mathematical equations?
- Scientific symbols?
- Complex diagrams?
- All those symbols you can't find on a standard keyboard?

But, the information is *right there* – just in the wrong format!

## Enter AuToTeX 
We've created what you've been waiting for: a **sleek, minimalist webapp** that automatically converts your handwritten documents into professional LaTeX files!

### What to like about AuToTeX?
- **Simple**: Just upload or jot down your handwritten notes
- **Smart**: Recognizes complex mathematical notation
- **Swift**: Converts in seconds
- **Stylish**: Outputs clean, professional LaTeX documents

No more spending hours transcribing your notes. No more hunting for that elusive integral symbol. Just your thoughts, professionally formatted and ready to share!

## Our Tech Stack 

Here's what makes AuToTeX tick:

- **Django** for the robust backend
- **Bootstrap** for slick styling
- **HTML/CSS/JS** to tie it all together
- **LangChain + OpenAI API** for the AI magic
- **MathTex** to compile our TeX

## Project Pipeline

1. **Input**: User uploads or draws handwritten notes in the web UI.
2. **Save**: Django stores document state/image (`Document` model).
3. **Inference**: `LaTeXGenerator` (`langchain_demos/constraint_gen.py`) sends the image and prompt template to a vision-capable LLM.
4. **Post-process**: The app strips markdown fences and writes `static/output.tex`.
5. **Compile**: `pdflatex` compiles TeX into `static/output.pdf`.
6. **Return**: Backend returns both LaTeX content and PDF (base64) to the frontend.

## Deploying AuToTeX

### 1) Install dependencies

```bash
pip install django djangorestframework openai python-dotenv opencv-python
```

Install a TeX compiler (for example TeX Live) so `pdflatex` is available.

### 2) Configure environment variables

```bash
export API_KEY="<your-openai-api-key>"
export OPENAI_MODEL="chatgpt-4o-latest"
# optional: OpenAI-compatible endpoint (self-hosted/custom serving)
export OPENAI_BASE_URL="https://api.openai.com/v1"
```

### 3) Run migrations and start app

```bash
python manage.py migrate
python manage.py runserver 0.0.0.0:8000
```

### 4) Production deployment basics

- Set `DEBUG=False`
- Restrict `ALLOWED_HOSTS`
- Serve static/media files from your web server or object storage
- Run with a production WSGI server (for example gunicorn + nginx)

## Using customized, fine-tuned, or reinforcement-trained models

- **Customized/fine-tuned OpenAI model**: set `OPENAI_MODEL` to your model ID (example: `ft:gpt-4o-mini:org:project:model-id`).
- **Reinforcement-trained or self-hosted model**: expose an OpenAI-compatible endpoint and set both:
  - `OPENAI_BASE_URL` to your endpoint
  - `OPENAI_MODEL` to the served model name
- No code changes are needed for switching models after this update; deployment-level env vars control model routing.

## Challenges we ran into
**Syncing and Saving Uploaded Image Files:** We struggled with managing edit histories and ensuring new edits were correctly compiled.

**Dynamic Code Editor:** Integrating an editable LaTeX interpreter required balancing real-time synchronization between frontend and backend interfaces.

## Accomplishments We're Proud Of 
**Developed a solution that addresses real needs:** Making online documents easier in a world that needs them!

**Integrating AI:** And it will only grow more helpful and popular! 

**Excelled in the UI design:** Our team of mostly backend developers crushed it with a minmalist design. 😎

## What we learned
**AI has fundamentaly changed creativity:** Creating new products has never been easier. Learning new frameworks has never been easier. And the capabilities of AI have only grown more impressive.

We're all very optimistic about AI. The rate at which it has improved is truly mindblowing.
****

## What's next for AuToTex
**Expanding to more users:** We truly believe our webapp will be useful for many outside of this hackathon and has many real world applications.

**Syncing the Canvas and Code:** Users should be able to bounce back and forth between debugging code and stylus 🖊️  
