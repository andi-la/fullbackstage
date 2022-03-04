## API Report File for "@backstage/plugin-search-backend-node"

> Do not edit this file. It is a report generated by [API Extractor](https://api-extractor.com/).

```ts
/// <reference types="node" />

import { DocumentCollatorFactory } from '@backstage/search-common';
import { DocumentDecoratorFactory } from '@backstage/search-common';
import { DocumentTypeInfo } from '@backstage/search-common';
import { IndexableDocument } from '@backstage/search-common';
import { Logger as Logger_2 } from 'winston';
import { default as lunr_2 } from 'lunr';
import { QueryTranslator } from '@backstage/search-common';
import { Readable } from 'stream';
import { SearchEngine } from '@backstage/search-common';
import { SearchQuery } from '@backstage/search-common';
import { SearchResultSet } from '@backstage/search-common';
import { Transform } from 'stream';
import { Writable } from 'stream';

// @beta
export abstract class BatchSearchEngineIndexer extends Writable {
  constructor(options: BatchSearchEngineOptions);
  abstract finalize(): Promise<void>;
  abstract index(documents: IndexableDocument[]): Promise<void>;
  abstract initialize(): Promise<void>;
}

// @beta (undocumented)
export type BatchSearchEngineOptions = {
  batchSize: number;
};

// @beta (undocumented)
export type ConcreteLunrQuery = {
  lunrQueryBuilder: lunr_2.Index.QueryBuilder;
  documentTypes?: string[];
  pageSize: number;
};

// @beta
export abstract class DecoratorBase extends Transform {
  constructor();
  abstract decorate(
    document: IndexableDocument,
  ): Promise<IndexableDocument | IndexableDocument[] | undefined>;
  abstract finalize(): Promise<void>;
  abstract initialize(): Promise<void>;
}

// @beta (undocumented)
export class IndexBuilder {
  constructor({ logger, searchEngine }: IndexBuilderOptions);
  addCollator({
    factory,
    defaultRefreshIntervalSeconds,
  }: RegisterCollatorParameters): void;
  addDecorator({ factory }: RegisterDecoratorParameters): void;
  build(): Promise<{
    scheduler: Scheduler;
  }>;
  // (undocumented)
  getDocumentTypes(): Record<string, DocumentTypeInfo>;
  // (undocumented)
  getSearchEngine(): SearchEngine;
}

// @beta (undocumented)
export type IndexBuilderOptions = {
  searchEngine: SearchEngine;
  logger: Logger_2;
};

// @beta (undocumented)
export type LunrQueryTranslator = (query: SearchQuery) => ConcreteLunrQuery;

// @beta (undocumented)
export class LunrSearchEngine implements SearchEngine {
  constructor({ logger }: { logger: Logger_2 });
  // (undocumented)
  protected docStore: Record<string, IndexableDocument>;
  // (undocumented)
  getIndexer(type: string): Promise<LunrSearchEngineIndexer>;
  // (undocumented)
  protected logger: Logger_2;
  // (undocumented)
  protected lunrIndices: Record<string, lunr_2.Index>;
  // (undocumented)
  query(query: SearchQuery): Promise<SearchResultSet>;
  // (undocumented)
  setTranslator(translator: LunrQueryTranslator): void;
  // (undocumented)
  protected translator: QueryTranslator;
}

// @beta (undocumented)
export class LunrSearchEngineIndexer extends BatchSearchEngineIndexer {
  constructor();
  // (undocumented)
  buildIndex(): lunr_2.Index;
  // (undocumented)
  finalize(): Promise<void>;
  // (undocumented)
  getDocumentStore(): Record<string, IndexableDocument>;
  // (undocumented)
  index(documents: IndexableDocument[]): Promise<void>;
  // (undocumented)
  initialize(): Promise<void>;
}

// @beta
export interface RegisterCollatorParameters {
  defaultRefreshIntervalSeconds: number;
  factory: DocumentCollatorFactory;
}

// @beta
export interface RegisterDecoratorParameters {
  factory: DocumentDecoratorFactory;
}

// @beta (undocumented)
export class Scheduler {
  constructor({ logger }: { logger: Logger_2 });
  addToSchedule(task: Function, interval: number): void;
  start(): void;
  stop(): void;
}

export { SearchEngine };

// @beta
export class TestPipeline {
  execute(): Promise<TestPipelineResult>;
  withDocuments(documents: IndexableDocument[]): TestPipeline;
  static withSubject(subject: Readable | Transform | Writable): TestPipeline;
}

// @beta
export type TestPipelineResult = {
  error: unknown;
  documents: IndexableDocument[];
};
```