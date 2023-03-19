import telegram
import requests

# Replace YOUR_BOT_TOKEN with your actual bot token
bot = telegram.Bot(token='6290165227:AAHQZySRbFj72nNKBSCjCZNn_PDoUWV4WBw')

# Replace YOUR_CHAT_ID with the ID of the chat you want to send the URLs to
chat_id = '1399730641'

# List of URLs to upload
url_list = [
    'https://example.com/image1.jpg',
    'https://example.com/image2.jpg',
    'https://example.com/image3.jpg',
]

# Loop through the URLs and upload each one to Telegram
for url in url_list:
    # Get the image data from the URL
    response = requests.get(url)
    image_data = response.content

    # Upload the image to Telegram and get the file ID
    file_id = bot.send_photo(chat_id=chat_id, photo=image_data)['photo'][-1]['file_id']

    # Construct the URL for the uploaded image
    url = f'https://api.telegram.org/file/bot{bot.token}/{file_id}'

    # Print the URL for the uploaded image
    print(url)
