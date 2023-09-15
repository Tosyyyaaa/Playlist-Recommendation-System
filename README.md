# Playlist-Recommendation-System
# Playlist recommendation/generation system(website), which caters a playlist to user’s preferences, by requesting favourite genre and artists, and learns from feedback provided by the user.

import random
import spotipy
from spotipy.oauth2 import SpotifyClientCredentials

# Replace with Spotify API credentials
SPOTIPY_CLIENT_ID = "YOUR_SPOTIFY_CLIENT_ID"
SPOTIPY_CLIENT_SECRET = "YOUR_SPOTIFY_CLIENT_SECRET"

# Initialize Spotipy with client credentials
sp = spotipy.Spotify(auth_manager=SpotifyClientCredentials(client_id=SPOTIPY_CLIENT_ID, client_secret=SPOTIPY_CLIENT_SECRET))

# Sample music data: replace this with your actual music data or fetched from a Spotify playlist
#fetch playlists from Spotify using sp.user_playlist_tracks(user_id, playlist_id)
music_data = [
    {"song": "Song 1", "artist": "Taylor Swift", "genre": "Pop"},
    {"song": "Song 2", "artist": "Ed Sheeran", "genre": "Pop"},
    {"song": "Song 3", "artist": "Ariana Grande", "genre": "Pop"},
    {"song": "Song 4", "artist": "Beyonce", "genre": "R&B"},
    {"song": "Song 5", "artist": "Drake", "genre": "Hip-Hop"},
    {"song": "song 6", "artist": "Louis Armstrong", "genre": "Jazz"},
    {"song": "song 7", "artist": "John Coltrane", "genre": "Jazz"},
    {"song": "song 8", "artist": "Miles Davis", "genre": "Jazz"}
    # Add more music data
]

def generate_playlist(user_genre, user_liked_artists, music_data, playlist_size=10):
    # Filter music data based on user preferences
    recommended_songs = []
    for song in music_data:
        if song["genre"] == user_genre or song["artist"] in user_liked_artists:
            recommended_songs.append(song)

    # Shuffle the recommended songs to simulate personalized recommendations
    random.shuffle(recommended_songs)

    # Return the first `playlist_size` songs as the generated playlist
    return recommended_songs[:playlist_size]

def display_playlist(playlist):
    print("Generated Playlist:")
    for index, song in enumerate(playlist):
        print(f"{index+1}. {song['song']} by {song['artist']} ({song['genre']})")

# Main function
def main():
    while True:
        # Ask the user for their favorite genre and liked artists
        user_favorite_genre = input("Enter your favorite music genre: ")
        user_liked_artists_input = input("Enter artists you like (comma-separated): ")
        user_liked_artists = [artist.strip() for artist in user_liked_artists_input.split(",")]

        # Generate a playlist for the user's preferences
        generated_playlist = generate_playlist(user_favorite_genre, user_liked_artists, music_data)

        # Display the generated playlist
        display_playlist(generated_playlist)

        # Ask the user if they want to regenerate the playlist
        regenerate = input("Do you want to regenerate the playlist? (yes/no): ")
        if regenerate.lower() != "yes":
            break

if __name__ == "__main__":
    main()
