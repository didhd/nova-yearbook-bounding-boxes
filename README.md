# Amazon Nova Pro - Yearbook Photo Bounding Box Detection

This notebook demonstrates how to use **Amazon Nova Pro** to detect individual portrait photos in yearbook grid layouts using natural language instructions.

## Overview

Traditional computer vision approaches struggle with dense yearbook photo grids where portraits are tightly packed together. Amazon Nova Pro's vision-language capabilities can understand contextual instructions like "detect individual portrait photos in this grid layout" to accurately identify each student photo separately.

## Features

- **Natural Language Instructions**: Use plain English to describe what to detect
- **Accurate Bounding Boxes**: Get precise coordinates for each individual portrait
- **Grid Layout Support**: Handles dense photo grids with minimal spacing
- **Zero Training Required**: No custom model training or labeled datasets needed
- **Structured JSON Output**: Easy-to-parse detection results

## Use Case

This solution is designed for:
- Yearbook digitization projects
- Photo extraction from grid layouts
- Student portrait tagging systems
- Batch processing of yearbook pages

## Prerequisites

- AWS Account with Amazon Bedrock access
- Amazon Nova Pro model enabled in your region
- Python 3.8+
- Jupyter Notebook environment

## Setup

1. **Clone this repository**
   ```bash
   git clone https://github.com/didhd/nova-yearbook-bounding-boxes.git
   cd nova-yearbook-bounding-boxes
   ```

2. **Install dependencies**
   ```bash
   pip install boto3 pillow matplotlib
   ```

3. **Configure AWS credentials**
   ```bash
   aws configure
   ```

4. **Enable Amazon Nova Pro**
   - Go to [Amazon Bedrock Console](https://console.aws.amazon.com/bedrock/home#/modelaccess)
   - Request access to Amazon Nova Pro model

## Usage

1. Open the Jupyter notebook:
   ```bash
   jupyter notebook Nova_Pro_Yearbook_BoundingBox.ipynb
   ```

2. Update the image path in the notebook:
   ```python
   yearbook_image_path = "./your_yearbook_page.jpg"
   ```

3. Run all cells to:
   - Load and display your yearbook image
   - Detect individual portrait photos
   - Visualize bounding boxes
   - Export results as JSON

## Example Output

```json
{
  "total_photos": 18,
  "photos": [
    {
      "id": "photo_1",
      "bounding_box": {
        "x_min": 120,
        "y_min": 150,
        "x_max": 280,
        "y_max": 350
      }
    }
  ]
}
```

## IAM Permissions

Ensure your AWS credentials have permission to invoke Bedrock models:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "bedrock:InvokeModel",
      "Resource": "arn:aws:bedrock:*::foundation-model/amazon.nova-pro-v1:0"
    }
  ]
}
```

## Cost Considerations

Amazon Nova Pro pricing (as of 2025):
- ~$0.003-0.005 per image
- For 100M yearbook pages: ~$300K-500K

Compare with:
- Amazon Textract Layout: $0.015 per page
- Bedrock Data Automation: $0.01 per page

## Architecture

```
Yearbook Image → Amazon Bedrock → Nova Pro → JSON Response → Visualization
```

## Advantages Over Traditional Approaches

| Feature | Nova Pro | Traditional CV | Textract Layout |
|---------|----------|----------------|-----------------|
| Grid Detection | ✅ Excellent | ❌ Poor | ⚠️ Limited |
| Natural Language | ✅ Yes | ❌ No | ❌ No |
| Training Required | ✅ No | ❌ Yes | ✅ No |
| Contextual Understanding | ✅ Yes | ❌ No | ⚠️ Limited |

## Troubleshooting

**Model Access Error**
- Verify Nova Pro is enabled in your AWS region
- Check IAM permissions for `bedrock:InvokeModel`

**Poor Detection Results**
- Ensure image resolution is adequate (recommended: 1500x2000+)
- Try adjusting the prompt for specific layout types
- Consider adding padding to bounding boxes (5-10%)

**JSON Parsing Errors**
- Check the raw model response in the notebook output
- Verify the response format matches expected structure

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## License

This project is licensed under the MIT-0 License - see the [LICENSE](LICENSE) file for details.

## Support

For questions or issues:
- Open a GitHub issue
- Contact AWS Support for Bedrock-related questions

## Related Resources

- [Amazon Bedrock Documentation](https://docs.aws.amazon.com/bedrock/)
- [Amazon Nova Models](https://aws.amazon.com/bedrock/nova/)
- [Bedrock Pricing](https://aws.amazon.com/bedrock/pricing/)

## Acknowledgments

Built with Amazon Nova Pro, a multimodal foundation model by AWS.
