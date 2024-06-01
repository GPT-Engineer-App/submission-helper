# submission-helper

provide me flutter code -   // Implement your file upload logic here
    // For example, you might want to use the file to create a submission
    // Navigator.push(context, MaterialPageRoute(builder: (context) => SubmissionPage(file: file)));


import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';

import 'package:pdf/widgets.dart' as pw;

import 'dart:io';

class HomeworkSubmissionPage extends StatefulWidget {
  const HomeworkSubmissionPage({super.key});

  @override
  // ignore: library_private_types_in_public_api
  _HomeworkSubmissionPageState createState() => _HomeworkSubmissionPageState();
}

class _HomeworkSubmissionPageState extends State<HomeworkSubmissionPage> {
  final ImagePicker _picker = ImagePicker();
  final List<XFile> _imageFiles = [];

  Future<void> _pickImage() async {
    final XFile? image = await _picker.pickImage(source: ImageSource.camera);
    if (image != null) {
      setState(() {
        _imageFiles.add(image);
      });
    }
  }

  Future<void> _createPdfAndUpload() async {
    final pdf = pw.Document();

    for (var imageFile in _imageFiles) {
      final image = pw.MemoryImage(File(imageFile.path).readAsBytesSync());
      pdf.addPage(pw.Page(build: (pw.Context context) {
        return pw.Center(child: pw.Image(image));
      }));
    }

    final output = await getTemporaryDirectory();
    final file = File("${output.path}/homework.pdf");
    await file.writeAsBytes(await pdf.save());

    // Implement your file upload logic here
    // For example, you might want to use the file to create a submission
    // Navigator.push(context, MaterialPageRoute(builder: (context) => SubmissionPage(file: file)));
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Submit Homework'),
        backgroundColor: Colors.amber, // Set the AppBar background color to amber
      ),
      body: Container(
        color: Colors.black, // Set the background color to black
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: <Widget>[
            const SizedBox(height: 20),
            const Text(
              'Instructions for submission:',
              style: TextStyle(color: Colors.white, fontSize: 18),
            ),
            const SizedBox(height: 10),
            const Text(
              '1. Ensure your homework is complete.\n2. Click the upload button to submit your homework.\n3. If you need more time, request a time extension.',
              style: TextStyle(color: Colors.white),
            ),
            const SizedBox(height: 20),
            Center(
              child: ElevatedButton.icon(
                onPressed: _pickImage,
                icon: const Icon(Icons.camera_alt),
                label: const Text('Take Image'),
                style: ElevatedButton.styleFrom(
                  backgroundColor: Colors.amber, // Set the button background color to amber
                ),
              ),
            ),
            const SizedBox(height: 10),
            Center(
              child: ElevatedButton.icon(
                onPressed: _createPdfAndUpload,
                icon: const Icon(Icons.picture_as_pdf),
                label: const Text('Create PDF & Upload'),
                style: ElevatedButton.styleFrom(
                  backgroundColor: Colors.amber, // Set the button background color to amber
                ),
              ),
            ),
            const SizedBox(height: 10),
            Center(
              child: OutlinedButton(
                onPressed: () {
                  // Handle time extension request logic
                },
                style: OutlinedButton.styleFrom(
                  foregroundColor: Colors.amber, side: const BorderSide(color: Colors.amber), // Set the button text color to amber
                ),
                child: const Text('Request Time Extension'),
              ),
            ),
            const Spacer(),
            const Center(
              child: Text(
                'Your homework has been successfully uploaded!',
                style: TextStyle(color: Colors.green, fontSize: 16),
              ),
            ),
            const SizedBox(height: 20),
          ],
        ),
      ),
    );
  }
  
  getTemporaryDirectory() async {}
}

void main() {
  runApp(const MaterialApp(
    home: HomeworkSubmissionPage(),
  ));
}

## Collaborate with GPT Engineer

This is a [gptengineer.app](https://gptengineer.app)-synced repository 🌟🤖

Changes made via gptengineer.app will be committed to this repo.

If you clone this repo and push changes, you will have them reflected in the GPT Engineer UI.

## Tech stack

This project is built with React and Chakra UI.

- Vite
- React
- Chakra UI

## Setup

```sh
git clone https://github.com/GPT-Engineer-App/submission-helper.git
cd submission-helper
npm i
```

```sh
npm run dev
```

This will run a dev server with auto reloading and an instant preview.

## Requirements

- Node.js & npm - [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating)
