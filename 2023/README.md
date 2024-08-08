# Canvas 2023 Data files
## canvas-2023-fixed-sql.sql
the sql file has 4 tables:
* colors (color_id, color_name, color_hex)
* pixels (log_id, user_id, x_cord, y_cord, color_id, time_placed, user_action)
* top_cord (top_cord_id, user_id, x_cord, y_cord, count_placed)
* users (user_id, username, ranking, total_pixels_placed)

The users table includes the rank and total pixels placed for each user. Deleted pixels are not counted.

The only data not included here is the pixel color counts for each user. You an find the pixel color counts for a user by selecting:

``SELECT color_name, count(color_name)
FROM public.pixels
JOIN users on users.user_id = pixels.user_id
JOIN colors on colors.color_id = pixels.color_id
WHERE username = <username> AND time_deleted IS NULL
GROUP BY color_name``

## color_count_2023.csv
The csv file used to serve user color counts to Canvas Stats. The columns are black, dark grey, deep grey, medium grey, light grey, white, beige, peach, brown, chocolate, rust, orange, yellow, pastel yellow, lime, green, dark green, forest, dark teal, light teal, aqua, azure, blue, navy, purple, mauve, magenta, pink, watermelon, red, rose, maroon.

## users_2023.csv
The csv file used to serve user data to Canvas stats. The columns are username, ranking, total pixels placed, x coordinate of top coordinte, y coordinate of top coordinate, and the number of pixels placed on top coordinate.