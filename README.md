# Improve the following code

You have a class that load the JSON from file, transform it and than save it back to file. Suggest the class improvements.

<!-- language: php -->
```
<?php

class FileTransformer {
    private $inputFile;
    private $outputFile;

    public function __construct($inputFile, $outputFile) {
        $this->inputFile = $inputFile;
        $this->outputFile = $outputFile;
    }

    public function transformFile() {
        try {
            // Load JSON content from file
            $jsonData = file_get_contents($this->inputFile);
            $dataArray = json_decode($jsonData, true);

            if ($dataArray === null) {
                throw new Exception("Invalid JSON format in input file.");
            }

            // Transform each element of the array (example: convert string values to uppercase)
            foreach ($dataArray as &$element) {
                if (is_string($element)) {
                    $element = strtoupper($element);
                }
            }

            // Convert the array back to JSON
            $transformedJson = json_encode($dataArray);

            if ($transformedJson === false) {
                throw new Exception("Failed to encode JSON after transformation.");
            }

            // Save transformed JSON to output file
            file_put_contents($this->outputFile, $transformedJson);
            
            return true;
        } catch (Exception $e) {
            // Log or handle the exception
            return false;
        }
    }
}

// Test Case
$inputFile = 'input.json'; // Assuming input file is in JSON format
$outputFile = 'output.json';

$fileTransformer = new FileTransformer($inputFile, $outputFile);
$result = $fileTransformer->transformFile();

if ($result) {
    echo "File transformed successfully!";
} else {
    echo "Failed to transform file. Check logs for details.";
}
?>
```
