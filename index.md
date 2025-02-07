import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Textarea } from "@/components/ui/textarea";
import { motion } from "framer-motion";
import { Button } from "@/components/ui/button";

export default function WordCounter() {
  const [text, setText] = useState("");

  const wordCount = text.trim() === "" ? 0 : text.trim().split(/\s+/).length;
  const charCount = text.replace(/\s/g, "").length; // Exclude spaces
  const spaceCount = (text.match(/ /g) || []).length;
  const syllableCount = text
    .toLowerCase()
    .split(/\s+/)
    .reduce((count, word) => count + (word.match(/[aeiouy]+/g) || []).length, 0);

  return (
    <div className="min-h-screen flex items-center justify-center bg-gradient-to-br from-purple-900 via-blue-900 to-black text-white p-4">
      <Card className="w-full max-w-2xl bg-gray-800 shadow-xl rounded-2xl p-6">
        <CardContent>
          <h1 className="text-3xl font-bold text-center mb-4">Lewit61 Word Counter</h1>
          <Textarea
            className="w-full p-4 text-lg bg-gray-700 text-white border-none rounded-xl focus:ring-2 focus:ring-blue-500 resize-none overflow-hidden"
            placeholder="Start typing..."
            value={text}
            onChange={(e) => {
              setText(e.target.value);
              e.target.style.height = "auto";
              e.target.style.height = e.target.scrollHeight + "px";
            }}
          />
          <div className="flex justify-between items-center mt-4">
            <p className="text-lg">Words: {wordCount}</p>
            <p className="text-lg">Characters (excluding spaces): {charCount}</p>
          </div>
          <div className="flex justify-between items-center mt-2">
            <p className="text-lg">Spaces: {spaceCount}</p>
            <p className="text-lg">Syllables: {syllableCount}</p>
          </div>
          <div className="flex justify-center mt-4">
            <Button
              onClick={() => setText("")}
              className="bg-blue-600 hover:bg-red-500 transition-colors text-white px-6 py-2 rounded-lg"
            >
              Clear Text
            </Button>
          </div>
        </CardContent>
      </Card>
      <motion.div
        className="fixed bottom-4 right-4 bg-gray-900 p-3 rounded-xl shadow-lg ring-4 ring-purple-500 ring-opacity-90 shadow-purple-500/75"
        whileHover={{ scale: 1.1 }}
      >
        <p className="text-sm text-gray-400">
          Created by 
          <a 
            href="https://lewit61productions.carrd.co" 
            target="_blank" 
            rel="noopener noreferrer" 
            className="text-blue-400 hover:underline ml-1"
          >
            Lewit61
          </a>
        </p>
      </motion.div>
    </div>
  );
}
