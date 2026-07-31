# automation/create_project.py
# Script to automatically create new project structure

import os
import sys
from pathlib import Path
from datetime import datetime

def create_project(project_name, project_type):
    """Create a new project with standard structure"""
    
    # Define project types and their default files
    templates = {
        'frontend': {
            'files': ['index.html', 'styles.css', 'script.js'],
            'folders': ['assets', 'images', 'css', 'js']
        },
        'shopify': {
            'files': ['theme.liquid', 'config.yml'],
            'folders': ['sections', 'templates', 'assets']
        },
        'java': {
            'files': ['Main.java', 'README.md'],
            'folders': ['src', 'classes', 'lib']
        }
    }
    
    # Create base directory
    os.makedirs(project_name, exist_ok=True)
    os.chdir(project_name)
    
    # Create folders
    template = templates.get(project_type, {})
    for folder in template.get('folders', []):
        os.makedirs(folder, exist_ok=True)
    
    # Create files with boilerplate
    for file in template.get('files', []):
        with open(file, 'w') as f:
            f.write(f"# {file}\n# Created: {datetime.now()}\n")
    
    print(f"✅ Created {project_name} ({project_type})")
    return project_name

if __name__ == "__main__":
    if len(sys.argv) < 3:
        print("Usage: python create_project.py <project_name> <project_type>")
        print("Types: frontend, shopify, java")
        sys.exit(1)
    
    create_project(sys.argv[1], sys.argv[2])
