Document Intelligence System - OneDrive to Supabase Vector Store

Overview

This n8n workflow automates the process of extracting documents from Microsoft OneDrive and indexing them into a Supabase vector database. The system enables semantic search capabilities across your documents using AI-powered embeddings, making it ideal for building intelligent document search, RAG (Retrieval Augmented Generation) applications, and knowledge management systems.

What This Workflow Does

The workflow searches for documents containing "EDIFY" in your OneDrive, downloads them, converts the content into vector embeddings using OpenAI, and stores them in a Supabase database. This allows you to perform semantic searches where you can find documents based on meaning rather than just keyword matching.

Use Cases

Knowledge Base Management - Build searchable company knowledge bases
Document Intelligence - Enable AI-powered document search and retrieval
Customer Support - Power chatbots with context from company documents
Research Systems - Create semantic search across research papers and documentation
Enterprise Search - Implement intelligent search across organizational documents

Workflow Architecture

Step 1: Manual Trigger
Initiates the workflow when you manually execute it from the n8n interface

Step 2: Search File in OneDrive
Searches Microsoft OneDrive for files matching the query "EDIFY"
Returns file metadata including ID, name, and location

Step 3: Download File
Downloads the matched file from OneDrive using the file ID
Retrieves the complete document content for processing

Step 4: Supabase Vector Store
Stores the processed document vectors in Supabase database
Inserts data into the "documents" table with embeddings

Step 5: OpenAI Embeddings
Converts document text into numerical vector representations
Uses OpenAI's embedding model for high-quality semantic understanding

Step 6: Default Data Loader
Processes the document and extracts content
Attaches metadata including the original filename

Prerequisites and Requirements

Required Accounts

n8n instance (cloud or self-hosted version 1.0 or higher)
Microsoft OneDrive account with documents to index
OpenAI API account with active credits
Supabase project with vector extension enabled

Required Credentials

Microsoft OneDrive OAuth2 API credentials
OpenAI API key
Supabase project URL and service key

Supabase Database Setup

Before running this workflow, ensure your Supabase database has:

A table named "documents" created
pgvector extension enabled
Proper columns for storing embeddings and metadata

Example Supabase table structure:

CREATE TABLE documents (
  id BIGSERIAL PRIMARY KEY,
  content TEXT,
  metadata JSONB,
  embedding VECTOR(1536)
);

Installation and Setup

Step 1: Import Workflow
Download the workflow JSON file from this repository
Open your n8n instance
Navigate to Workflows and click Import
Upload the JSON file

Step 2: Configure Credentials
Click on "Search a file" node
Add your Microsoft OneDrive OAuth2 credentials
Click on "Embeddings OpenAI" node
Add your OpenAI API key
Click on "Supabase Vector Store" node
Add your Supabase project URL and service key

Step 3: Verify Database Connection
Ensure the "documents" table exists in Supabase
Verify the table name matches in the workflow configuration
Test the connection by executing the workflow

Step 4: Prepare Your Documents
Upload documents to your OneDrive
Ensure documents contain "EDIFY" in their name or content
Supported formats include PDF, DOCX, TXT, and more

How to Use

Basic Usage

Open the workflow in n8n
Click "Execute workflow" button
The workflow will search for matching files
Documents will be downloaded and processed
Vectors will be stored in your Supabase database

Monitoring Execution

Check the execution log for each node
Verify files were found in OneDrive
Confirm successful embedding generation
Validate data insertion in Supabase

Configuration and Customization

Changing Search Query

Locate the "Search a file" node
Modify the "query" parameter from "EDIFY" to your desired search term
Save the workflow

Example:
"query": "2024 Reports"
"query": "Contract"
"query": "Invoice"

Selecting Different Vector Store Table

Open "Supabase Vector Store" node
Change "tableName" to your preferred table
Ensure the table has the correct schema

Adding Custom Metadata

Open "Default Data Loader" node
Navigate to metadata configuration
Add new metadata fields as needed

Example metadata fields:
- file_name: Original document name
- upload_date: When document was processed
- file_type: Document format
- department: Document category

Changing Embedding Model

Open "Embeddings OpenAI" node
Select different model from options
Consider cost and performance tradeoffs

Advanced Features

Batch Processing
Modify the workflow to process multiple files simultaneously by removing filters

Scheduled Execution
Add a Schedule Trigger node to run the workflow automatically at set intervals

Error Notifications
Integrate email or Slack notifications for failed executions

Content Filtering
Add filtering nodes to process only specific file types or sizes

Troubleshooting Guide

Common Issues and Solutions

No Files Found
Check that documents exist in OneDrive with the search term
Verify OneDrive credentials are valid and authenticated
Ensure proper permissions are granted to the API

Download Failures
Confirm file ID is correctly passed between nodes
Check network connectivity to OneDrive
Verify file is not corrupted or locked

Embedding Errors
Ensure OpenAI API key is valid and has credits
Check document content is extractable text
Verify API rate limits are not exceeded

Supabase Connection Issues
Confirm project URL and service key are correct
Check that the documents table exists
Verify pgvector extension is enabled

Metadata Not Saving
Review metadata configuration in Default Data Loader
Ensure JSONB column exists in Supabase table
Check for special characters in metadata values

Performance Optimization

Document Size Management
Split large documents into smaller chunks for better embedding quality
Implement pagination for processing multiple files

Caching Strategy
Store processed file IDs to avoid reprocessing
Implement checksum validation for changed documents

Rate Limiting
Add delay nodes between API calls to respect rate limits
Implement retry logic for failed requests

Security Considerations

Credential Management
Store all API keys and credentials in n8n's credential manager
Never expose credentials in workflow configurations or logs

Data Privacy
Ensure compliance with data protection regulations
Review what data is being sent to OpenAI for embedding
Implement access controls on Supabase tables

API Security
Use environment-specific credentials
Rotate API keys regularly
Monitor API usage for anomalies

Integration Possibilities

Connect with ChatGPT
Use stored vectors to provide context for AI conversations

Build Search Interface
Create a frontend that queries the Supabase vector store

Integrate with Slack
Allow team members to search documents via Slack commands

Connect to CRM
Automatically process and index customer-related documents

Technical Specifications

Supported File Formats
PDF, DOCX, TXT, MD, CSV, and other text-based formats

Vector Dimensions
OpenAI embeddings: 1536 dimensions (text-embedding-ada-002)

Database Requirements
PostgreSQL with pgvector extension
Minimum Supabase plan: Free tier supported

API Rate Limits
OpenAI: Varies by plan
Microsoft Graph API: Throttling limits apply

Contributing

Contributions are welcome. To contribute:

Fork this repository
Create a feature branch
Make your changes
Submit a pull request with detailed description

License

This workflow is provided as-is under MIT License for both personal and commercial use.

Support and Community

For issues, questions, or feature requests, please open an issue in this repository.

Version History

Version 1.0 - Initial release with basic OneDrive to Supabase integration
Future updates will include batch processing and enhanced error handling

Acknowledgments

Built with n8n workflow automation platform
Powered by OpenAI embeddings
Uses Supabase as vector database backend
