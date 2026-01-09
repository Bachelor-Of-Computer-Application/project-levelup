# LevelUp Backend API - Bruno Collection

This is a complete Bruno collection for the LevelUp Backend API.

## Setup

1. Install Bruno from https://www.usebruno.com/
2. Open Bruno and click "Open Collection"
3. Navigate to this folder and open it
4. Update the `token` variable in the Local environment after logging in

## Environment Variables

The collection uses the following environment variables (configured in `environments/Local.bru`):

- `base_url`: The base URL for the API (default: http://localhost:8001/api/v1)
- `token`: Your authentication token (set automatically after login or manually)

## Folders

- **Auth**: Authentication and user management endpoints
- **Community**: Community CRUD operations and member management
- **Admin**: Admin-only endpoints for managing users, communities, categories, and tickets
- **Clan**: Clan management within communities
- **AI**: AI chat and quest generation endpoints
- **Ticket**: Support ticket management
- **Leaderboard**: Various leaderboard endpoints
- **Health**: System health check

## Quick Start

1. **Register a new account**: Auth → Register
2. **Login**: Auth → Login (this will automatically set the token)
3. **Get your profile**: Auth → Get Me
4. **Create a community**: Community → Create Community
5. **Explore other endpoints**

## Notes

- Most endpoints require authentication (Bearer token)
- Admin endpoints require admin privileges
- File upload endpoints use multipart/form-data
- Replace placeholder values (e.g., `community_id_here`, `user_id_here`) with actual IDs

## Total Endpoints: 100+

### Auth (13 endpoints)
- Register, Login, Logout
- Password management (forgot, reset, change)
- Email verification
- Profile picture upload
- OAuth registration
- Onboarding

### Community (17 endpoints)
- CRUD operations
- Member management
- Join/leave communities
- Role management
- Messages
- Photo upload

### Admin (19 endpoints)
- User management
- Community management
- Category management
- Ticket management
- Analytics and stats

### Clan (11 endpoints)
- Create, update, delete clans
- Join/leave clans
- Member management
- Messages

### AI (25 endpoints)
- Chat with AI
- Quest generation (daily/weekly)
- Quest management
- Admin operations

### Ticket (5 endpoints)
- CRUD operations for support tickets

### Leaderboard (5 endpoints)
- Global, community, and clan leaderboards
- Top communities and clans

### Health (1 endpoint)
- System health check

## Support

For issues or questions, please refer to the API documentation or contact the development team.
