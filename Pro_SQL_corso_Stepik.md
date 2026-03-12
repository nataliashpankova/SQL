--CREARE TABELLE--------------------------------------

CREATE TABLE users(
    id INT PRIMARY KEY UNIQUE AUTO_INCREMENT NOT NULL,
    full_name VARCHAR(50) NOT NULL,
    details VARCHAR(50),
    join_date DATE NOT NULL,
    avatar TEXT,
    is_active BOOLEAN NOT NULL,
    knowledge INT DEFAULT 0 NOT NULL,
    reputation INT DEFAULT 0 NOT NULL,
    followers_count INT DEFAULT 0 NOT NULL,
    days_without_break INT DEFAULT 0 NOT NULL,
    days_without_break_max INT DEFAULT 0 NOT NULL,
    solved_tasks INT DEFAULT 0 NOT NULL
);

CREATE TABLE courses(
    id INT PRIMARY KEY UNIQUE NOT NULL AUTO_INCREMENT,
    title VARCHAR(50) NOT NULL,
    created_date DATE NOT NULL,
    summary TEXT,
    photo TEXT,
    price DECIMAL(10, 2)
);

CREATE TABLE user_courses(
    user_id INT,
    course_id INT,
    is_favorite BOOLEAN,
    is_pinned BOOLEAN,
    is_archived BOOLEAN,
    last_viewed DATE,
    
    PRIMARY KEY(user_id, course_id),
    
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (course_id) REFERENCES courses(id)
);
