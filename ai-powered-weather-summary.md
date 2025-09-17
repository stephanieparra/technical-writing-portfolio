# Adding AI-Powered Weather Summaries to the React Weather App

This guide shows how to enhance the React Weather App by integrating a lightweight AI workflow that generates human-friendly weather summaries based on the existing API data. This document explains a mock version of integrating the friendly AI weather summary in [this React Weather App project](https://github.com/stephanieparra/react-weather-app) so that API keys for LLMs can stay secure.

---

## 1. Why Add an AI-enhanced, Humanized Summary to a Weather App?

- **Human-centered UX** → turns raw weather data into natural language insights that feel intuitive, friendly, and approachable.

- **Practical AI integration** → demonstrates that we can wire AI into existing React components with minimal overhead.

- **Real-world relevance** → connects APIs and AI to deliver a polished product, highlighting both technical skill and conceptual thinking for future AI use cases in existing (as well as non-existent) apps.

- **Recruiter/enterprise value** → demonstrates innovative thinking, problem-solving, and familiarity with modern AI-augmented workflows.
---

## 2. Install Dependencies

For this example, we’ll use OpenAI’s API to generate summaries, however, you can use the LLM you prefer. In your terminal, install the dependency:
```
npm install openai
```

## 3. Create the AI Utility

In your src folder, create a file called aiSummary.js. In this component, you'll create a variable for the prompt: 
```
import OpenAI from "openai";

const client = new OpenAI({
  apiKey: process.env.REACT_APP_OPENAI_API_KEY, // set in .env
});

export async function generateWeatherSummary(weatherData) {
  const prompt = `
  Given this weather data: 
  - City: ${weatherData.city}
  - Temp: ${weatherData.temperature}°F
  - Condition: ${weatherData.description}
  - Humidity: ${weatherData.humidity}%
  - Wind: ${weatherData.wind} km/h
  
  Write a short, friendly summary for a user. Keep it under 40 words.
  `;

  const response = await client.chat.completions.create({
    model: "gpt-4o-mini",
    messages: [{ role: "user", content: prompt }],
  });

  return response.choices[0].message.content.trim();
}
```
## 4. Wire Into the Component

Update WeatherInfo.js to call the AI summary and render it below the weather details.
```
import React, { useEffect, useState } from "react";
import FormattedDate from "./FormattedDate";
import WeatherIcon from "./WeatherIcon";
import WeatherTemperature from "./WeatherTemperature";
import { generateWeatherSummary } from "./aiSummary";

export default function WeatherInfo(props) {
  const [aiSummary, setAiSummary] = useState("");

  useEffect(() => {
    async function fetchSummary() {
      const summary = await generateWeatherSummary(props.data);
      setAiSummary(summary);
    }
    fetchSummary();
  }, [props.data]);

  return (
    <div className="WeatherInfo">
      <h1>{props.data.city}</h1>
      <ul>
        <li>
          <FormattedDate date={props.data.date} />
        </li>
        <li className="text-capitalize">{props.data.description}</li>
      </ul>
      <div className="row mt-3">
        <div className="col-6">
          <div className="d-flex">
            <div>
              <WeatherIcon code={props.data.icon} size={52} />
            </div>
            <div>
              <WeatherTemperature fahrenheit={props.data.temperature} />
            </div>
          </div>
        </div>
        <div className="col-6">
          <ul>
            <li>Humidity: {props.data.humidity}%</li>
            <li>Wind: {props.data.wind}/km</li>
          </ul>
        </div>
      </div>

      /* AI-Powered Weather Summary */
      {aiSummary && (
        <div className="ai-summary mt-3">
          <strong>AI Summary:</strong> {aiSummary}
        </div>
      )}
    </div>
  );
}
```
---
## 5. Example Output

Instead of only showing raw numbers, users now see a friendly summary like:

> ️🌤️ "It’s a sunny 72°F in Los Angeles with light winds — perfect for a walk!"

