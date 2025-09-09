erDiagram

    user {
    string id PK
    string firstName
    string lastName
    string email
    string userType
    string unitAddress
    }

    Channel {
        string id PK
        string title
        date createdAt
        boolean isPrivate
    }

    ChannelMembership {
        string id PK
        string channelId FK
        string userId
        date joinedAt
        string role
    }

    Message {
        string id PK
        string sentBy
        string content
        enum messageType 'channel, direct'
        string entityId FK 'channelid, sentTo'
        boolean isPinned
        date sentAt
        boolean isForwarded
    }

    Thread {
        string id PK
        string content
        string parentMessageId FK
        string sentBy FK
        date createdAt
        boolean isPinned
    }

    reactions {
        string id PK
        string reaction
        string reactedBy FK
        boolean isThread
        enum entityType 'message, thread'
        string entityId FK
        date createdAt
    }

    media {
        string id PK
        string messageId FK
        string threadId FK
        boolean isThread
        string uploadedBy FK
        string url
        string fileType
        date uploadedAt
    }

    %% Relationships
    user ||--o{ ChannelMembership : "id < userId"
    Channel ||--o{ ChannelMembership : "id < channelId"
    user ||--o{ Message : "id < sentBy"
    Channel ||--o{ Message : "id < entityId"
    user ||--o{ Message : "id < entityId"
    Message ||--o{ Thread : "id < parentMessageId"
    user ||--o{ Thread : "id < sentBy"
    Message ||--o{ media : "id < messageId"
    Thread ||--o{ media : "id < threadId"
    user ||--o{ media : "id < uploadedBy"
    user ||--o{ reactions : "id < reactedBy"
    Message ||--o{ reactions : "id < entityId"
    Thread ||--o{ reactions : "id < entityId"

link - https://app.eraser.io/workspace/l9wB1eIVooTHTdBkCqyD?origin=share&elements=0JKVN0b-MoNJaN325bpc8g
