## Security & Privacy

All data stays local on your machine:

- No external API calls to Langfuse cloud
- No data transmission to third parties
- Models and traces stored in local Docker volumes
- Review `.env.dev.example` for configuration secrets to set

### Setup Security

1. Copy `.env.dev.example` to `.env`
2. Generate new secrets: `openssl rand -hex 32`
3. Update ENCRYPTION_KEY and NEXTAUTH_SECRET
4. **Never commit `.env` file to git**
