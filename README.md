# Setting Up YouTube AI Summarizer
This tutorial will guide you through setting up and running your YouTube AI Summarizer on both Windows using Laragon and Linux/Mac.

## Prerequisites
- A machine with PHP, Python, and a web server (Apache or Nginx) installed

## Step 1: Download the Project from GitHub
- Download the project files from GitHub. Open a web browser and navigate to the project repository on GitHub [placeholder].
- Extract the downloaded files to your web server's root directory:
  - For Windows using Laragon: `C:\laragon\www\youtube-ai-summarizer`
  - For Linux/Mac: `/var/www/html/youtube-ai-summarizer`

## Step 2: Configure Python Environment
- Install the required Python modules. Open a terminal or command prompt and navigate to your project directory:
  - Navigate to the project directory: `cd path/to/your/project/youtube-ai-summarizer`
  - Install the required Python modules: `pip install -r requirements.txt`

## Step 3: Update PHP Scripts
- Add your OpenAI API key in `summarize.php`. Update the line `define('API_KEY', 'your-openai-key-here');` with your actual API key.
- Modify the system prompt in `summarize.php` if needed. Update the line `"content" => "You will be provided with video transcript, and your task is to summarize the transcripts as follows:\n\n-Overall summary of video\n-Key Points (what one needs to do if applicable and how). Try to put some concise bullet points with a brief intro paragraph."` to customize the prompt.

## Step 4: Configure Your Web Server to Use Python
### For Laragon (Windows)
- Configure Laragon to recognize Python scripts. Open the `httpd.conf` file for Apache, which can be found in `C:\laragon\bin\apache\httpd-2.4.39\conf` (the version number might be different).
- Add the following lines to enable CGI (Common Gateway Interface):
  ```apache
  ScriptAlias /cgi-bin/ "C:/laragon/www/youtube-ai-summarizer/"
  <Directory "C:/laragon/www/youtube-ai-summarizer">
      AllowOverride None
      Options +ExecCGI
      Require all granted
      AddHandler cgi-script .py
  </Directory>

- Save the file and restart Apache via Laragon.

### For Linux/Mac
- Configure Apache to recognize Python scripts. Open the Apache configuration file, which could be `httpd.conf` or a site-specific configuration file in `/etc/apache2/sites-available/`.
- Add the following lines to enable CGI (Common Gateway Interface):
  ```apache
  ScriptAlias /cgi-bin/ "/var/www/html/youtube-ai-summarizer/"
  <Directory "/var/www/html/youtube-ai-summarizer">
      AllowOverride None
      Options +ExecCGI
      Require all granted
      AddHandler cgi-script .py
  </Directory>

Save the file and restart Apache: `sudo systemctl restart apache2`

## Step 5: Testing
- Access your web application:
  - For Windows using Laragon: Open a web browser and navigate to `http://localhost/youtube-ai-summarizer`
  - For Linux/Mac: Open a web browser and navigate to `http://localhost/youtube-ai-summarizer`
- Enter a YouTube video ID and click 'Get Transcript'.
- Click 'Summarize' to get the summarized text.

## Project Structure
- `index.php`: Default page that loads the form.
- `youtube.php`: Script called by `index.php` form action to retrieve the transcript.
- `summarize.php`: Script called to summarize the transcript and populate the summary textarea.
- `youtube.py`: Python script to fetch YouTube transcripts.

## Notes
- Ensure you replace placeholder values (e.g., `your-openai-key-here`) with actual values.
- Adjust the Apache configuration according to your setup if needed.

## Minimum Requirements
- A web server (Apache or Nginx)
- PHP
- Python with required modules (`requirements.txt`)

