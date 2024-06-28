import axios, { AxiosError } from 'axios';

// Define the data type for the request payload
interface PostData {
  title: string;
  body: string;
  userId: number;
}

// Define the data type for the response
interface PostResponse {
  id: number;
  title: string;
  body: string;
  userId: number;
}

async function makePostRequest(data: PostData): Promise<void> {
  try {
    const response = await axios.post<PostResponse>('https://jsonplaceholder.typicode.com/posts', data);
    console.log('Response data:', response.data);
  } catch (error) {
    handleAxiosError(error);
  }
}

function handleAxiosError(error: AxiosError): void {
  if (error.response) {
    // The request was made and the server responded with a status code that falls out of the range of 2xx
    console.error('Response error data:', error.response.data);
    console.error('Response error status:', error.response.status);
    console.error('Response error headers:', error.response.headers);
  } else if (error.request) {
    // The request was made but no response was received
    console.error('No response received:', error.request);
  } else {
    // Something happened in setting up the request that triggered an Error
    console.error('Error in request setup:', error.message);
  }
  console.error('Error config:', error.config);
}

// Example data to post
const postData: PostData = {
  title: 'foo',
  body: 'bar',
  userId: 1,
};

// Make the POST request
makePostRequest(postData);
