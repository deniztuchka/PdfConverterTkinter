import tkinter as tk
from tkinter import filedialog, messagebox
from PyPDF2 import PdfMerger, PdfReader
from pdf2image import convert_from_path
import os


# Function to merge PDFs
def merge_pdfs():
    files = filedialog.askopenfilenames(filetypes=[("PDF files", "*.pdf")])
    if not files:
        return
    merger = PdfMerger()
    for file in files:
        merger.append(file)
    output_file = filedialog.asksaveasfilename(defaultextension=".pdf", filetypes=[("PDF files", "*.pdf")])
    if output_file:
        merger.write(output_file)
        merger.close()
        messagebox.showinfo("Success", "PDFs merged successfully!")


# Function to extract text from PDF
def extract_text():
    file = filedialog.askopenfilename(filetypes=[("PDF files", "*.pdf")])
    if not file:
        return
    reader = PdfReader(file)
    extracted_text = "\n".join([page.extract_text() for page in reader.pages if page.extract_text()])
    text_window = tk.Toplevel(root)
    text_window.title("Extracted Text")
    text_box = tk.Text(text_window, wrap="word")
    text_box.insert("1.0", extracted_text)
    text_box.pack(expand=True, fill="both")


# Function to convert PDF to image
def convert_pdf():
    file = filedialog.askopenfilename(filetypes=[("PDF files", "*.pdf")])
    if not file:
        return
    output_folder = filedialog.askdirectory()
    if not output_folder:
        return

    # Specify poppler path for Windows users
    poppler_path = None  # Change this if needed on Windows
    images = convert_from_path(file, poppler_path=poppler_path)
    for i, img in enumerate(images):
        img_path = os.path.join(output_folder, f"page_{i + 1}.png")
        img.save(img_path, "PNG")
    messagebox.showinfo("Success", "PDF converted to images successfully!")


# Tkinter UI setup
root = tk.Tk()
root.title("PDF Editor & Converter")
root.geometry("400x300")

tk.Label(root, text="PDF Editor & Converter", font=("Arial", 14)).pack(pady=10)

tk.Button(root, text="Merge PDFs", command=merge_pdfs).pack(pady=5)
tk.Button(root, text="Extract Text from PDF", command=extract_text).pack(pady=5)
tk.Button(root, text="Convert PDF to Images", command=convert_pdf).pack(pady=5)
tk.Button(root, text="Exit", command=root.quit).pack(pady=20)

root.mainloop()
