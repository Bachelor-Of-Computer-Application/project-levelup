# LevelUp Backend API Routes Documentation

Complete API routes documentation for the LevelUp Backend application.

**Base URL**: `http://localhost:8001/api/v1`

---

## Table of Contents

- [Authentication Routes](#authentication-routes)
- [Community Routes](#community-routes)
- [Admin Routes](#admin-routes)
- [Clan Routes](#clan-routes)
- [AI Routes](#ai-routes)
- [Ticket Routes](#ticket-routes)
- [Leaderboard Routes](#leaderboard-routes)
- [Health Routes](#health-routes)

---

## Authentication Routes

**Base Path**: `/api/v1/auth`

### User Registration & Authentication

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `POST` | `/register` | ❌ | Register a new user account |
| `POST` | `/login` | ❌ | Login with email and password |
| `POST` | `/oauth/register` | ❌ | Register/Login with OAuth (Google, etc.) |
| `POST` | `/logout` | ✅ | Logout current user |
| `POST` | `/deleteAccount` | ✅ | Delete user account permanently |

### Password Management

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `POST` | `/forget-password` | ❌ | Request password reset email |
| `POST` | `/reset-password` | ❌ | Reset password with token |
| `POST` | `/change-password` | ✅ | Change password for logged-in user |

### User Profile

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `GET` | `/me` | ✅ | Get current user profile |
| `POST` | `/verify-email` | ❌ | Verify email with token |
| `POST` | `/upload-profile-picture` | ✅ | Upload user profile picture |
| `POST` | `/onBoarding` | ✅ | Complete user onboarding |

### Categories

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `GET` | `/categories` | ❌ | Fetch all available categories |

---

## Community Routes

**Base Path**: `/api/v1/community`

### Community Management

| Method | Endpoint | Auth Required | Admin Only | Description |
|--------|----------|---------------|------------|-------------|
| `POST` | `/create` | ✅ | ❌ | Create a new community with optional photo |
| `GET` | `/` | ✅ | ❌ | Get all public communities |
| `GET` | `/my` | ✅ | ❌ | Get user's joined communities |
| `GET` | `/search` | ✅ | ❌ | Search communities by name |
| `GET` | `/:communityId` | ✅ | ❌ | Get specific community details |
| `PATCH` | `/:communityId` | ✅ | ❌ | Update community details (owner/admin) |
| `POST` | `/:communityId/upload-photo` | ✅ | ❌ | Upload/update community photo |

### Community Membership

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `POST` | `/:communityId/join` | ✅ | Join a public community |
| `POST` | `/join` | ✅ | Join a private community with join code |
| `POST` | `/:communityId/leave` | ✅ | Leave a community |
| `GET` | `/:communityId/owner` | ✅ | Get community owner info |
| `GET` | `/:communityId/members` | ✅ | Get all community members |

### Community Administration

| Method | Endpoint | Auth Required | Role Required | Description |
|--------|----------|---------------|---------------|-------------|
| `POST` | `/:communityId/transfer-ownership` | ✅ | Owner | Transfer community ownership (newOwnerId = userId or CommunityMember ID) |
| `DELETE` | `/:communityId/members/:memberId` | ✅ | Admin | Remove a member from community (memberId = userId or CommunityMember ID) |
| `PATCH` | `/:communityId/members/:memberId/role` | ✅ | Admin | Change member role (memberId = userId or CommunityMember ID) |

### Community Features

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `POST` | `/toggle-pin` | ✅ | Toggle pin for multiple communities |
| `GET` | `/:communityId/messages` | ✅ | Get community messages with pagination |

---

## Admin Routes

**Base Path**: `/api/v1/admin`

**Note**: All admin routes require authentication + admin role

### Dashboard & Analytics

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/overview` | Get admin dashboard overview |
| `GET` | `/user-growth` | Get user growth statistics |

### User Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/users/all` | Get all users with pagination |
| `GET` | `/users/:id` | View specific user details |
| `PATCH` | `/users/:id` | Update user details |
| `DELETE` | `/users/delete` | Delete a user account |

### Community Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/communities/stats` | Get community statistics |
| `GET` | `/communities/all` | Get all communities with filters |
| `GET` | `/communities/:communityId/members` | Get community members |
| `PUT` | `/communities/:communityId` | Update community details |
| `DELETE` | `/communities/:communityId` | Delete a community |
| `DELETE` | `/communities/:communityId/members/:memberId` | Remove community member |
| `PATCH` | `/communities/:communityId/privacy` | Change community privacy |
| `PATCH` | `/communities/:communityId/category` | Change community category |

### Category Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/categories/stats` | Get category statistics |
| `POST` | `/communities/addCategory` | Add new category |
| `PUT` | `/categories/:oldName` | Edit category name |
| `DELETE` | `/categories/:categoryName` | Delete a category |

### Ticket Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| `PUT` | `/ticket/:id` | Update ticket status and details |

---

## Clan Routes

**Base Path**: `/api/v1/clan`

### Clan Management

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `POST` | `/create` | ✅ | Create a new clan in a community |
| `GET` | `/:communityId` | ✅ | Get all clans in a community |
| `GET` | `/info/:clanId` | ✅ | Get specific clan information |
| `PUT` | `/:clanId` | ✅ | Update clan details |
| `DELETE` | `/:clanId` | ✅ | Delete a clan |

### Clan Membership

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `POST` | `/join` | ✅ | Join a clan |
| `POST` | `/leave` | ✅ | Leave a clan |
| `GET` | `/members/:clanId` | ✅ | Get clan members |
| `GET` | `/user/:userId` | ✅ | Get user's clans |
| `GET` | `/checkMembership/:clanId` | ✅ | Check if user is clan member |

### Clan Communication

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `GET` | `/clan/:clanId/messages` | ✅ | Get clan messages (under /community path) |

---

## AI Routes

**Base Path**: `/api/v1/ai`

### AI Chat

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `POST` | `/chat` | ✅ | Send message to AI assistant |
| `GET` | `/chat/history` | ✅ | Get chat history with pagination |
| `GET` | `/chat/tokens` | ✅ | Get user's token balance |
| `DELETE` | `/chat/history` | ✅ | Delete all chat history (with ?all=true) |
| `DELETE` | `/chat/history/:chatId` | ✅ | Delete specific chat by ID |

### Quest Generation

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `POST` | `/generate/daily` | ✅ | Generate daily quests for user |
| `POST` | `/generate/weekly` | ✅ | Generate weekly quests for user |
| `POST` | `/generate/daily/force` | ✅ | Force regenerate daily quests |
| `POST` | `/generate/weekly/force` | ✅ | Force regenerate weekly quests |

### Quest Management

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `GET` | `/quests/daily` | ✅ | Get user's daily quests |
| `GET` | `/quests/weekly` | ✅ | Get user's weekly quests |
| `GET` | `/quests/completed` | ✅ | Get completed quests with pagination |
| `GET` | `/quests/:questId` | ✅ | Get single quest details |
| `POST` | `/quests/start` | ✅ | Start a quest |
| `PATCH` | `/quests/complete` | ✅ | Mark quest as completed |
| `DELETE` | `/quests/:questId` | ✅ (Admin) | Delete a quest |

### AI System

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `GET` | `/health` | ✅ | AI system health check |
| `GET` | `/config` | ✅ | Get AI configuration |
| `GET` | `/community/memberships` | ✅ | Get community memberships with XP |

### AI Admin Operations

| Method | Endpoint | Auth Required | Admin Required | Description |
|--------|----------|---------------|----------------|-------------|
| `POST` | `/admin/generate/daily/all` | ✅ | ✅ | Generate daily quests for all users |
| `POST` | `/admin/generate/daily/:userId` | ✅ | ✅ | Generate daily quests for specific user |
| `POST` | `/admin/generate/weekly/all` | ✅ | ✅ | Generate weekly quests for all users |
| `POST` | `/admin/generate/weekly/:userId` | ✅ | ✅ | Generate weekly quests for specific user |
| `GET` | `/admin/quests/stats` | ✅ | ✅ | Get quest statistics |
| `DELETE` | `/admin/quests` | ✅ | ✅ | Bulk delete quests |

---

## Ticket Routes

**Base Path**: `/api/v1/ticket`

### Ticket Management

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `POST` | `/create` | ✅ | Create a new support ticket |
| `GET` | `/` | ✅ | Get all tickets by user |
| `GET` | `/:id` | ✅ | Get ticket by ID |
| `PUT` | `/:id` | ✅ | Update ticket by ID |
| `DELETE` | `/:id` | ✅ | Delete ticket by ID |

---

## Leaderboard Routes

**Base Path**: `/api/v1/leaderboard`

### Leaderboards

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `GET` | `/` | ✅ | Get global user leaderboard |
| `GET` | `/community/:communityId` | ✅ | Get community leaderboard (members by XP) |
| `GET` | `/top-communities` | ✅ | Get top communities (sortBy: xp/members/createdAt) |
| `GET` | `/clan/:clanId` | ✅ | Get clan leaderboard (members by XP) |
| `GET` | `/top-clans` | ✅ | Get top clans (with optional communityId filter) |

---

## Health Routes

**Base Path**: `/api/v1/health`

### System Health

| Method | Endpoint | Auth Required | Description |
|--------|----------|---------------|-------------|
| `GET` | `/` | ❌ | System health check |

---

## Common Request/Response Patterns

### Authentication Header

```
Authorization: Bearer <your_token_here>
```

### Language Header

```
x-language: eng
```

Supported languages: `eng`, `ar`, etc.

### Common Response Format

**Success Response:**
```json
{
  "success": true,
  "message": "Operation successful",
  "data": { ... },
  "statusCode": 200
}
```

**Error Response:**
```json
{
  "success": false,
  "error": "Error message",
  "message": "Translated error message",
  "statusCode": 400
}
```

### Pagination Parameters

Many list endpoints support pagination:

```
?page=1&limit=10
```

### Sorting Parameters

Some endpoints support sorting:

```
?sortBy=createdAt&order=desc
```

---

## File Upload Endpoints

The following endpoints accept multipart/form-data for file uploads:

1. **Profile Picture Upload**: `/api/v1/auth/upload-profile-picture`
   - Field name: `profilePicture`
   - Accepted formats: JPG, PNG, etc.

2. **Community Creation**: `/api/v1/community/create`
   - Field name: `photo`
   - Optional field

3. **Community Photo Upload**: `/api/v1/community/:communityId/upload-photo`
   - Field name: `photo`

---

## Status Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---

## Rate Limiting

- AI Chat endpoints have token-based rate limiting
- Check token balance via `/api/v1/ai/chat/tokens`

---

## Notes

1. **Authentication**: Most endpoints require Bearer token authentication
2. **Admin Routes**: Require both authentication and admin role
3. **Role-Based Access**: Some community operations require ADMIN or Owner role
4. **Private Communities**: Require join code for access
5. **File Uploads**: Use multipart/form-data content type
6. **Pagination**: Default page size varies by endpoint
7. **Quest System**: AI-generated quests refresh daily/weekly based on cron jobs

---

## Environment

- **Development**: `http://localhost:8001/api/v1`
- **Production**: Update base URL accordingly

---

## Total Endpoints: 100+

- **Auth**: 13 endpoints
- **Community**: 17 endpoints  
- **Admin**: 19 endpoints
- **Clan**: 11 endpoints
- **AI**: 25 endpoints
- **Ticket**: 5 endpoints
- **Leaderboard**: 5 endpoints
- **Health**: 1 endpoint

---

**Last Updated**: January 2, 2026

**API Version**: 1.0.0
