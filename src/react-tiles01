import React, { useState, useCallback } from 'react';
import { useNavigate } from 'react-router-dom';

interface TileData {
  id: number;
  title: string;
  imageUrl: string;
  caption: string;
  detailedCaption: string;
  isLiked: boolean;
}

const initialTiles: TileData[] = [
    { id: 1, title: "First Tile", imageUrl: "", caption: "A short caption for the first tile", detailedCaption: "This is a more detailed caption for the first tile, providing additional information and context. It can be very long!", isLiked: false },
    { id: 2, title: "Second Tile", imageUrl: "", caption: "A short caption for the second tile", detailedCaption: "This is a more detailed caption for the second tile, providing additional information and context.", isLiked: false },
    { id: 3, title: "Third Tile", imageUrl: "", caption: "A short caption for the third tile", detailedCaption: "This is a more detailed caption for the third tile, providing additional information and context. It can be really really long and be something like a blog!", isLiked: false },
    { id: 4, title: "Fourth Tile", imageUrl: "", caption: "A short caption for the fourth tile", detailedCaption: "This is a more detailed caption for the fourth tile, providing additional information and context.", isLiked: false },
    { id: 5, title: "Fifth Tile", imageUrl: "", caption: "A short caption for the fifth tile", detailedCaption: "This is a more detailed caption for the fifth tile, providing additional information and context.", isLiked: false },
    { id: 6, title: "Sixth Tile", imageUrl: "", caption: "A short caption for the sixth tile", detailedCaption: "This is a more detailed caption for the sixth tile, providing additional information and context.", isLiked: false },
    { id: 7, title: "Seventh Tile", imageUrl: "", caption: "A short caption for the seventh tile", detailedCaption: "This is a more detailed caption for the seventh tile, providing additional information and context.", isLiked: false },
    { id: 8, title: "Eighth Tile", imageUrl: "", caption: "A short caption for the eighth tile", detailedCaption: "This is a more detailed caption for the eighth tile, providing additional information and context.", isLiked: false },
    { id: 9, title: "Ninth Tile", imageUrl: "", caption: "A short caption for the ninth tile", detailedCaption: "This is a more detailed caption for the ninth tile, providing additional information and context.", isLiked: false },
];


interface TileGridProps {
  tilesPerRow: number;
}

const TileGrid: React.FC<TileGridProps> = ({ tilesPerRow }) => {
  const [tiles, setTiles] = useState<TileData[]>(initialTiles);
  const navigate = useNavigate();

  const handleTileClick = useCallback((tileId: number) => {
    navigate(`/tile/${tileId}`);
  }, [navigate]);


  const handleLike = useCallback((tileId: number) => {
      setTiles((prevTiles) =>
          prevTiles.map((tile) =>
              tile.id === tileId ? { ...tile, isLiked: !tile.isLiked } : tile
          )
      );
  }, [setTiles]);


  const chunkedTiles = Array(Math.ceil(tiles.length / tilesPerRow))
      .fill(null)
      .map((_, index) => tiles.slice(index * tilesPerRow, (index + 1) * tilesPerRow));


  return (
      <div className="container mx-auto p-4">
          {chunkedTiles.map((row, rowIndex) => (
              <div key={rowIndex} className="flex flex-wrap justify-center mb-4">
                  {row.map((tile) => (
                      <div key={tile.id} className={`w-full sm:w-1/2 md:w-1/${tilesPerRow} lg:w-1/${tilesPerRow} p-2`}>
                          <div className="bg-white rounded-lg shadow-md overflow-hidden flex flex-col h-full">
                              <div className="p-4 flex items-center justify-between">
                                  <h2 className="text-xl font-semibold text-gray-800">{tile.title}</h2>
                                  <button onClick={() => handleLike(tile.id)}>
                                      <svg
                                          xmlns="http://www.w3.org/2000/svg"
                                          className={`h-6 w-6 ${tile.isLiked ? 'fill-red-500 text-red-500' : 'text-gray-400'}`}
                                          viewBox="0 0 24 24"
                                          stroke="currentColor"
                                      >
                                          <path
                                              strokeLinecap="round"
                                              strokeLinejoin="round"
                                              strokeWidth={2}
                                              d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"
                                          />
                                      </svg>
                                  </button>
                              </div>
                              <div onClick={() => handleTileClick(tile.id)} className="cursor-pointer flex-grow flex flex-col items-center justify-center p-4">
                                  {tile.imageUrl ? (
                                      <img src={tile.imageUrl} alt={tile.title} className="w-full h-auto object-cover rounded-md mb-2" />
                                  ) : (
                                      <div className="bg-gray-200 border-2 border-dashed rounded-xl w-full h-32 mb-2 flex items-center justify-center">
                                        <span className="text-gray-500">No Image</span>
                                    </div>
                                  )}
                                <p className="text-gray-700 text-center text-sm">{tile.caption}</p>
                              </div>
                          </div>
                      </div>
                  ))}
              </div>
          ))}
      </div>
  );
};


const TileDetail: React.FC = () => {
  const { id } = useParams<{id: string}>();
  const tileId = parseInt(id || '', 10);

  const tile = initialTiles.find(tile => tile.id === tileId);

    if (!tile) {
        return <div className="container mx-auto p-4">Tile not found</div>;
    }

    return (
        <div className="container mx-auto p-4">
            <div className="bg-white rounded-lg shadow-md p-6">
              <h1 className="text-2xl font-bold mb-4 text-gray-800">{tile.title}</h1>
                {tile.imageUrl ? (
                    <img src={tile.imageUrl} alt={tile.title} className="w-full h-auto object-cover rounded-md mb-4" />
                ) : (
                    <div className="bg-gray-200 border-2 border-dashed rounded-xl w-full h-64 mb-4 flex items-center justify-center">
                        <span className="text-gray-500">No Image</span>
                    </div>
                )}
              <p className="text-gray-700">{tile.detailedCaption}</p>
            </div>
        </div>
    );
};

import { BrowserRouter as Router, Route, Routes, useParams } from 'react-router-dom';
const App: React.FC = () => {
    return (
      <Router>
        <Routes>
          <Route path="/" element={<TileGrid tilesPerRow={3} />} />
          <Route path="/tile/:id" element={<TileDetail />} />
        </Routes>
      </Router>
    );
};


export default App;