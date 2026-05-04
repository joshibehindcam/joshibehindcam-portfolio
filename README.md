# joshibehindcam-portfolio
import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion, AnimatePresence } from "framer-motion";

const images = [
  { id: 1, category: "cars", src: "https://picsum.photos/900/1200?random=1" },
  { id: 2, category: "people", src: "https://picsum.photos/800/1000?random=2" },
  { id: 3, category: "architecture", src: "https://picsum.photos/1000/800?random=3" },
  { id: 4, category: "cars", src: "https://picsum.photos/800/1200?random=4" },
  { id: 5, category: "people", src: "https://picsum.photos/900/1100?random=5" },
  { id: 6, category: "architecture", src: "https://picsum.photos/1100/900?random=6" },
];

export default function Portfolio() {
  const [filter, setFilter] = useState("all");
  const [selectedIndex, setSelectedIndex] = useState(null);

  const filteredImages =
    filter === "all" ? images : images.filter((img) => img.category === filter);

  const nextImage = () => {
    setSelectedIndex((prev) => (prev + 1) % filteredImages.length);
  };

  const prevImage = () => {
    setSelectedIndex((prev) =>
      prev === 0 ? filteredImages.length - 1 : prev - 1
    );
  };

  return (
    <div className="min-h-screen bg-white text-gray-900">
      {/* Hero */}
      <section className="h-screen flex flex-col justify-center items-center text-center px-4">
        <motion.h1
          initial={{ opacity: 0, y: 40 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 1 }}
          className="text-6xl md:text-8xl font-extrabold tracking-tight mb-4"
        >
          Joshibehindcam
        </motion.h1>
        <motion.p
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
          transition={{ delay: 0.5 }}
          className="text-lg text-gray-500"
        >
          Automotive · Portrait · Architecture
        </motion.p>
      </section>

      {/* Filter */}
      <section className="flex justify-center gap-6 mb-12 text-sm uppercase tracking-widest">
        {["all", "cars", "people", "architecture"].map((cat) => (
          <button
            key={cat}
            onClick={() => setFilter(cat)}
            className={`pb-1 border-b-2 transition ${
              filter === cat ? "border-black" : "border-transparent text-gray-400"
            }`}
          >
            {cat}
          </button>
        ))}
      </section>

      {/* Masonry Gallery */}
      <section className="columns-1 md:columns-3 gap-6 px-6 space-y-6">
        {filteredImages.map((img, index) => (
          <motion.img
            key={img.id}
            src={img.src}
            className="w-full rounded-2xl cursor-pointer hover:opacity-90 transition"
            whileHover={{ scale: 1.02 }}
            onClick={() => setSelectedIndex(index)}
          />
        ))}
      </section>

      {/* Lightbox Advanced */}
      <AnimatePresence>
        {selectedIndex !== null && (
          <motion.div
            className="fixed inset-0 bg-black/90 flex items-center justify-center z-50"
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            exit={{ opacity: 0 }}
          >
            <button
              className="absolute left-6 text-white text-3xl"
              onClick={prevImage}
            >
              ‹
            </button>

            <motion.img
              key={filteredImages[selectedIndex].id}
              src={filteredImages[selectedIndex].src}
              className="max-h-[80vh] rounded-xl"
              initial={{ scale: 0.9, opacity: 0 }}
              animate={{ scale: 1, opacity: 1 }}
              exit={{ scale: 0.9, opacity: 0 }}
            />

            <button
              className="absolute right-6 text-white text-3xl"
              onClick={nextImage}
            >
              ›
            </button>

            <button
              className="absolute top-6 right-6 text-white text-xl"
              onClick={() => setSelectedIndex(null)}
            >
              ✕
            </button>
          </motion.div>
        )}
      </AnimatePresence>

      {/* About */}
      <section className="px-6 py-24 max-w-2xl mx-auto text-center">
        <h2 className="text-4xl font-semibold mb-6">About</h2>
        <p className="text-gray-500 leading-relaxed">
          I capture moments, machines, and spaces with a modern and cinematic approach. Replace this with your personal story.
        </p>
      </section>

      {/* Contact */}
      <section className="px-6 pb-24 text-center">
        <h2 className="text-3xl font-semibold mb-6">Contact</h2>
        <Button className="rounded-full px-8 py-6 text-lg">Email Me</Button>
      </section>

      <footer className="py-8 text-center text-gray-400 text-sm">
        © {new Date().getFullYear()} Joshibehindcam
      </footer>
    </div>
  );
}
